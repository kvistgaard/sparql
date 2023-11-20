type:: [[Function/On strings]]

- Checks if a [language tags]([[Language tags]]) matches a language range
- `FILTER (LANG(?label) = "fr")` will only return results where the language tag of `?label` is `@fr`, while `FILTER langMATCHES( LANG(?label), "fr" )` will also include those with regions such as `@fr-BE`.