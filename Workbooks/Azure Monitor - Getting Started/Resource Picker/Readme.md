# <a name="picking-a-set-of-resources-to-analyze-in-workbooks"></a>Auswählen einer Gruppe zu analysierender Ressourcen in Arbeitsmappen

Die Vorlage `Resource Picker` stellt Abonnement-, Ressourcengruppen- und Ressourcenparameter zum Einrichten des Eingabekontexts Ihrer Arbeitsmappe bereit. Mit den Standardparametern werden virtuelle Computer ausgewählt. Sie kann jedoch für einen beliebigen Ressourcentyp konfiguriert werden. Die Vorlage verfügt auch über ein ARG-Abfragesteuerelement, das zeigt, wie Sie die Parameter in Ihren Analysen verwenden.

![Image](Full.png)

## <a name="setting-up-the-resource-type-to-pick"></a>Einrichten des auszuwählenden Ressourcentyps

1. Wählen Sie auf der Arbeitsmappen-Symbolleiste die Option `Edit` aus.
2. Vor `Subscriptions` wird die Dropdownliste `Resource type` angezeigt:

    ![Image](Parameter.png)
3. Erweitern Sie die Dropdownliste, und wählen Sie die gewünschten Ressourcentypen aus. Daraufhin werden die Dropdownlisten für Abonnement, Ressourcengruppe und Ressourcen entsprechend aktualisiert.
4. Klicken Sie rechts unten in der Parametersteuerung auf die Schaltfläche `Edit`.
5. Ändern Sie im Parameterraster in der Zeile `Resources` die Spalte `Display name` von _Virtuelle Computer_ in den Anzeigenamen des ausgewählten Ressourcentyps (beispielsweise _Speicherkonten_).
6. Klicken Sie auf der Arbeitsmappen-Symbolleiste auf `Done Editing`.

## <a name="selecting-more-or-less-than-10-resources-by-default"></a>Standardmäßiges Auswählen von mehr oder weniger als zehn Ressourcen

1. Wählen Sie auf der Arbeitsmappen-Symbolleiste die Option `Edit` aus.
2. Klicken Sie rechts unten in der Parametersteuerung auf die Schaltfläche `Edit`.
3. Wählen Sie im Parameterraster die Zeile für `Resources` aus.
4. Klicken Sie auf der Symbolleiste auf `Edit` (Stiftsymbol).
5. Scrollen Sie im daraufhin angezeigten Bereich `Edit Parameter` nach unten zum Editor `Azure Resource Graph Query`. Dort sollte sich eine Abfrage wie die folgende befinden:
    ```sql
    Resources
    | where type in~({ResourceTypes})
    | extend resourceGroupId = strcat('/subscriptions/', subscriptionId, '/resourceGroups/', resourceGroup)
    | where resourceGroupId in~({ResourceGroups}) or '*' in~({ResourceGroups})
    | order by name asc
    | extend Rank = row_number()
    | project value = id, label = name, selected = Rank <= 10, group = resourceGroup
    ```
    Der Code für die Ressourcenauswahl befindet sich in der letzten Zeile der Abfrage: `selected = Rank <= 10`. 

6. Ändern Sie den Wert von „10“ in einen anderen Wert, um die Standardauswahl zu ändern.