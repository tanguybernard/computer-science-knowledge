# Proxy

## Protective Proxy

    public interface Internet
    {
        public void connectTo(String serverhost) throws Exception;
    }


    public class RealInternet implements Internet
    {
        @Override
        public void connectTo(String serverhost)
        {
            System.out.println("Connecting to "+ serverhost);
        }
    }


  Proxy

    public class ProxyInternet implements Internet
    {
        private Internet internet = new RealInternet();
        private static List<String> bannedSites;
          
        static
        {
            bannedSites = new ArrayList<String>();
            bannedSites.add("abc.com");
            bannedSites.add("def.com");
            bannedSites.add("ijk.com");
            bannedSites.add("lnm.com");
        }
          
        @Override
        public void connectTo(String serverhost) throws Exception
        {
            if(bannedSites.contains(serverhost.toLowerCase()))
            {
                throw new Exception("Access Denied");
            }
              
            internet.connectTo(serverhost);
        }
      
    }


main

    public class Client
    {
        public static void main (String[] args)
        {
            Internet internet = new ProxyInternet();
            try
            {
                internet.connectTo("geeksforgeeks.org");//Connecting to geeksforgeeks.org
                internet.connectTo("abc.com");//Access Denied
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
            }
        }
    }

source: https://www.geeksforgeeks.org/proxy-design-pattern/

## Virtual Proxy  

Le modèle de Virtual Proxy  est une technique d'économie de mémoire qui recommande de différer la création d'un objet jusqu'à ce qu'il soit nécessaire ;


    public interface Image {
    
    	public void showImage();
    	
    }


Real subject


    public class HighResolutionImage implements Image {
    
    	public HighResolutionImage(String imageFilePath) {
    		
    		loadImage(imageFilePath);
    	}
    
    	private void loadImage(String imageFilePath) {
    
    		// load Image from disk into memory
    		// this is heavy and costly operation
    	}
    
    	@Override
    	public void showImage() {
    
    		// Actual Image rendering logic
    
    	}
    
    }

Proxy

    public class ImageProxy implements Image {
    	private String imageFilePath;
    	
    	/**
    	 * Reference to RealSubject
    	 */
    	private Image proxifiedImage;
    	
    	
    	public ImageProxy(String imageFilePath) {
    		this.imageFilePath= imageFilePath;	
    	}
    	
    	@Override
    	public void showImage() {
    
    		// create the Image Object only when the image is required to be shown
    		
    		proxifiedImage = new HighResolutionImage(imageFilePath);
    		
    		// now call showImage on realSubject
    		proxifiedImage.showImage();
    		
    	}
    
    }

Main

public class ImageViewer {

	
    	public static void main(String[] args) {
    		
    	// assuming that the user selects a folder that has 3 images	
    	//create the 3 images 	
    	Image highResolutionImage1 = new ImageProxy("sample/veryHighResPhoto1.jpeg");
    	Image highResolutionImage2 = new ImageProxy("sample/veryHighResPhoto2.jpeg");
    	Image highResolutionImage3 = new ImageProxy("sample/veryHighResPhoto3.jpeg");
    	
    	// assume that the user clicks on Image one item in a list
    	// this would cause the program to call showImage() for that image only
    	// note that in this case only image one was loaded into memory
    	highResolutionImage1.showImage();
    	
    	// consider using the high resolution image object directly
    	Image highResolutionImageNoProxy1 = new HighResolutionImage("sample/veryHighResPhoto1.jpeg");
    	Image highResolutionImageNoProxy2 = new HighResolutionImage("sample/veryHighResPhoto2.jpeg");
    	Image highResolutionImageBoProxy3 = new HighResolutionImage("sample/veryHighResPhoto3.jpeg");
    	
    	
    	// assume that the user selects image two item from images list
    	highResolutionImageNoProxy2.showImage();
    	
    	// note that in this case all images have been loaded into memory 
    	// and not all have been actually displayed
    	// this is a waste of memory resources
    	
    	}
    		
    }

source: https://www.oodesign.com/proxy-pattern

## Remote proxy



## Proxy vs Decorator

A decorator implementation can be the same as the proxy however a decorator adds responsibilities to an object while a proxy controls access to it.
