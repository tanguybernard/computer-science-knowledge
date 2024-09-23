## Test Thymeleaf avec SpringTemplateEngine et Itext


## Code 


    package fr.entreprise.project.orderservice.infra.driven.contract;
    
    import com.itextpdf.html2pdf.HtmlConverter;
    import com.itextpdf.kernel.pdf.*;
    import com.itextpdf.io.font.constants.StandardFonts;
    import com.itextpdf.kernel.font.PdfFontFactory;
    import com.itextpdf.layout.Document;
    import com.itextpdf.layout.element.Paragraph;
    import com.itextpdf.layout.properties.TextAlignment;
    import com.itextpdf.layout.properties.VerticalAlignment;
    import fr.edf.tipienergy.orderservice.domain.order.Order;
    import fr.edf.tipienergy.orderservice.domain.order.User;
    import fr.edf.tipienergy.orderservice.domain.order.ports.ContractSpi;
    import fr.edf.useed.annotations.HexagonalArchitecture;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import org.springframework.core.io.ClassPathResource;
    import org.springframework.stereotype.Component;
    import org.springframework.util.FileCopyUtils;
    import org.thymeleaf.context.Context;
    import org.thymeleaf.spring6.SpringTemplateEngine;
    import reactor.core.publisher.Mono;
    
    import java.io.*;
    
    @Component
    @HexagonalArchitecture.RightAdapter
    public class ContractAdapter implements ContractSpi {
        private static final Logger logger = LoggerFactory.getLogger(ContractAdapter.class);
    
        private static final String TEMPLATE_BASE_PATH = "contrat-templates/";
        private static final String TEMPLATE_BASE_CPV_PATH = "contracts/";
    
        private final MergePdfUtil mergePdfUtil;
    
        private final SpringTemplateEngine templateEngine;
        private final ContractMapper contractMapper;
    
        public ContractAdapter(SpringTemplateEngine templateEngine, MergePdfUtil mergePdfUtil, ContractMapper contractMapper) {
            this.mergePdfUtil = mergePdfUtil;
            this.templateEngine = templateEngine;
            this.contractMapper = contractMapper;
        }
    
        @Override
        public Mono<byte[]> generateProfessionalCpvContract(Order order, User user, Boolean signed, String contractFile) {
            Context context = new Context();
            context.setVariables(this.contractMapper.dataModelForProfessionalCpvContract(order, user, signed));
    
            return generatePdfFrom(context, contractFile);
        }
    
        @Override
        public Mono<byte[]> generateIndividualCpvContract(Order order, User user, Boolean signed, String contractFile) {
            Context context = new Context();
            context.setVariables(this.contractMapper.dataModelForIndividualCpvContract(order, user, signed));
    
            return generatePdfFrom(context, contractFile);
        }
    
        private Mono<byte[]> generatePdfFrom(Context context, String contractFile) {
            return Mono.fromCallable(() -> {
    
                StringBuilder templatePath = new StringBuilder(TEMPLATE_BASE_CPV_PATH);
                templatePath.append(contractFile);
                String htmlContent = templateEngine.process(templatePath.toString(), context);
    
                ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
    
                HtmlConverter.convertToPdf(
                        htmlContent,
                        outputStream
                );
    
                return outputStream.toByteArray();
            });
        }
    
        @Override
        public Mono<byte[]> concatPdfDocuments(byte[] cpvPdf, byte[] cgvPdf) {
            return Mono.just(this.mergePdfUtil.concatPdfDocuments(cpvPdf, cgvPdf));
        }
    
        @Override
        public Mono<byte[]> addWatermarkToPdf(byte[] pdfBytes, String watermarkText) {
            try {
                var baos = new ByteArrayOutputStream();
                var pdfReader = new PdfReader(new ByteArrayInputStream(pdfBytes));
                var pdfWriter = new PdfWriter(baos);
                var pdfDoc = new PdfDocument(pdfReader, pdfWriter);
                var document = new Document(pdfDoc);
    
                var watermarkParagraph = new Paragraph(watermarkText)
                        .setFont(PdfFontFactory.createFont(StandardFonts.HELVETICA_BOLD))
                        .setFontSize(60)
                        .setOpacity(0.1f);
    
                for (int pageNumber = 1; pageNumber <= pdfDoc.getNumberOfPages(); pageNumber++) {
                    var page = pdfDoc.getPage(pageNumber);
                    float positionX = page.getPageSize().getWidth() / 2;
                    float positionY = page.getPageSize().getHeight() / 2;
    
                    document.showTextAligned(
                            watermarkParagraph,
                            positionX,
                            positionY,
                            pageNumber,
                            TextAlignment.CENTER,
                            VerticalAlignment.MIDDLE,
                            45
                    );
                }
    
                document.close();
                pdfDoc.close();
    
                return Mono.just(baos.toByteArray());
            } catch (Exception e) {
                return Mono.error(new RuntimeException("Error occurred when adding watermark to PDF"));
            }
        }
    
        @Override
        public Mono<byte[]> getFileAsByteArray(String path) {
            return Mono.create(monoSink -> {
                try {
                    var classPathResource = new ClassPathResource(TEMPLATE_BASE_PATH + path);
                    var bytes = FileCopyUtils.copyToByteArray(classPathResource.getInputStream());
                    monoSink.success(bytes);
                } catch (Exception e) {
                    logger.error(e.getMessage());
                    monoSink.error(new RuntimeException("Cannot read file from path : " + path));
                }
            });
        }
    
    }



## TEst

    package fr.entreprise.project.orderservice.infra.driven.contract;
    
    import com.itextpdf.kernel.pdf.PdfDocument;
    import com.itextpdf.kernel.pdf.PdfReader;
    import com.itextpdf.kernel.pdf.canvas.parser.PdfTextExtractor;
    import fr.edf.tipienergy.orderservice.domain.order.*;
    
    import fr.edf.tipienergy.orderservice.utils.builders.OrderTestBuilder;
    import org.junit.jupiter.api.BeforeEach;
    import org.junit.jupiter.api.Test;
    
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.autoconfigure.ImportAutoConfiguration;
    import org.springframework.boot.autoconfigure.thymeleaf.ThymeleafAutoConfiguration;
    import org.springframework.boot.test.context.SpringBootTest;
    import reactor.core.publisher.Mono;
    import reactor.test.StepVerifier;
    import org.thymeleaf.spring6.SpringTemplateEngine;
    
    import java.io.ByteArrayInputStream;
    import java.time.LocalDateTime;
    import java.time.format.DateTimeFormatter;
    import java.util.ArrayList;
    import java.util.List;
    import java.util.UUID;
    
    
    import static org.assertj.core.api.Assertions.assertThat;
    
    @SpringBootTest(classes = {ContractAdapter.class, ContractMapper.class, SpringTemplateEngine.class, MergePdfUtil.class}) //import uniquement les dépendances utiles au test
    @ImportAutoConfiguration(ThymeleafAutoConfiguration.class) //pour que Thymeleaf soit correctement configuré et aille chercher les templates htlml dans le bon repertoire
    class ContractAdapterTest {
    
    
        @Autowired
        private ContractAdapter contractAdapter;
    
    
        private Order mockOrder;
        private User mockUser;
    
        @BeforeEach
        void setUp() {
    
            mockOrder = aValidOrderWithStatusAndCustomerType();
            mockUser = new User("test@email.com");
        }
    
        @Test
        void testGenerateIndividualCpvContractWithSignaturecontainsSpecificWords() {
            String contractFile = "cpv_part_template.html";
            boolean signed = true;
    
            Mono<byte[]> resultMono = contractAdapter.generateIndividualCpvContract(mockOrder, mockUser, signed, contractFile);
    
            StepVerifier.create(resultMono)
                    .expectNextMatches(bytes -> {
                        try {
                            if (bytes.length == 0) {
                                return false;
                            }
    
                            PdfDocument pdfDoc = new PdfDocument(new PdfReader(new ByteArrayInputStream(bytes)));
    
                            // Extraction du texte du PDF
                            StringBuilder pdfText = new StringBuilder();
                            for (int i = 1; i <= pdfDoc.getNumberOfPages(); i++) {
                                pdfText.append(PdfTextExtractor.getTextFromPage(pdfDoc.getPage(i)));
                            }
    
                            pdfDoc.close();
    
                            LocalDateTime paidDate = mockOrder.events().stream().filter(event -> event.name().equals(OrderEventName.ORDER_PAID)).map(OrderEvent::date).findFirst().orElse(LocalDateTime.now());
                            DateTimeFormatter dateFormatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
                            DateTimeFormatter timeFormatter = DateTimeFormatter.ofPattern("HH:mm");
                            String formattedDate = paidDate.format(dateFormatter);
                            String formattedTime = paidDate.format(timeFormatter);
                            String signatureDatePresent = "Fait le " + formattedDate + " à " + formattedTime;
    
                            assertThat(pdfText.toString()).contains(
                                    "John DOE",
                                    signatureDatePresent,
                                    "120.0 Euros");
    
                            return true;
                        } catch (Exception e) {
                            e.printStackTrace();
                            return false;
                        }
                    })
                    .verifyComplete();
        }
    
        @Test
        void testGenerateIndividualCpvContractWithoutSignature_containsSpecificWords() {
            String contractFile = "cpv_part_template.html";
            boolean signed = false;
    
            Mono<byte[]> resultMono = contractAdapter.generateIndividualCpvContract(mockOrder, mockUser, signed, contractFile);
    
            // Utilisation de StepVerifier pour vérifier les résultats réactifs
            StepVerifier.create(resultMono)
                    .expectNextMatches(bytes -> {
                        try {
                            if (bytes.length == 0) {
                                return false;
                            }
    
                            // Lire le PDF en mémoire
                            PdfDocument pdfDoc = new PdfDocument(new PdfReader(new ByteArrayInputStream(bytes)));
    
                            // Extraction du texte du PDF
                            StringBuilder pdfText = new StringBuilder();
                            for (int i = 1; i <= pdfDoc.getNumberOfPages(); i++) {
                                pdfText.append(PdfTextExtractor.getTextFromPage(pdfDoc.getPage(i)));
                            }
    
                            pdfDoc.close();
    
                            LocalDateTime paidDate = mockOrder.events().stream().filter(event -> event.name().equals(OrderEventName.ORDER_PAID)).map(OrderEvent::date).findFirst().orElse(LocalDateTime.now());
                            DateTimeFormatter dateFormatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
                            String formattedDate = paidDate.format(dateFormatter);
                            String signatureDatePresent = "Fait le " + formattedDate;
    
                            assertThat(pdfText.toString()).contains(
                                    "John DOE",
                                    "120.0 Euros");
    
                            assertThat(pdfText.toString()).doesNotContain(signatureDatePresent);
    
                            return true;
                        } catch (Exception e) {
                            e.printStackTrace();
                            return false;
                        }
                    })
                    .verifyComplete();
        }
    
    
        private Order aValidOrderWithStatusAndCustomerType() {
    
            var delivery = new Delivery(
                    "John",
                    "Doe",
                    "1 rue de Paris",
                    "appartement 1",
                    "Paris",
                    "75000",
                    "FR4712739000708632776748V65"
            );
    
            ArrayList<OrderEvent> events = new ArrayList<>();
    
    
            OrderEvent orderPaid = new OrderEvent(OrderEventName.ORDER_PAID, UUID.randomUUID(), LocalDateTime.now(), OrderStatus.WAITING_FOR_ADMIN_VALIDATION);
            events.add(orderPaid);
    
            return OrderTestBuilder.anOrder()
                    .withEvents(events)
                    .withDefaultCustomer(CustomerType.INDIVIDUAL)
                    .withOffers(List.of(
                            new Offer(1, "standard", 2, "Centrale Drom Ramasse", 120.0, OrderTestBuilder.createDefaultTiwatts()),
                            new Offer(2, "special", 1, "Centrale Vannes", 100.0, OrderTestBuilder.createDefaultTiwatts())
    
                    ))
                    .withDelivery(delivery)
                    .withEvents(events)
                    .build();
    
    
        }
    }

