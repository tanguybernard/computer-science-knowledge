# Kotlin

## Callback de gestion d'erreur

- Permet de propager les erreurs de parsing sans utiliser d'exceptions
- Transmet les messages d'erreur contextualisés à l'appelant


```kotlin
fun createDateParser(zoneId: ZoneId): (String, (String) -> Unit) -> LocalDate? {
    return { text, onError ->
        try {
            when {
                text.isExcelEpochFormatted() -> 
                    DateUtil.getJavaDate(text.toDouble())
                        .toInstant()
                        .atZone(zoneId)
                        .toLocalDate()
                
                text.isNaturalDateFormatted() -> 
                    LocalDate.parse(text, DateTimeFormatter.ofPattern("[dd/MM/yyyy][d/M/yyyy]"))
                
                else -> {
                    onError("Format invalide")
                    null
                }
            }
        } catch (e: Exception) {
            onError("Erreur de conversion: ${e.message ?: "inconnue"}")
            null
        }
    }
}
```

```kotlin
val defaultParser = createDateParser(projectProperties.zoneId)

// Dans validateDate:
val parsedDate = defaultParser(colonne) { error -> 
    erreurs.add(ColonneValidationException("date.format", "$columnName - $error"))
}
```

Le pattern vient de l'idiome Kotlin qui privilégie les lambdas aux exceptions pour le contrôle de flux.

*Un idiome de programmation (ou programming idiom en anglais) désigne une manière conventionnelle et optimale d'exprimer une logique ou une structure dans un langage spécifique.*
