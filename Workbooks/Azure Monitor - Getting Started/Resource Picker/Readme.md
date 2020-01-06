# <a name="picking-a-set-of-resources-to-analyze-in-workbooks"></a><span data-ttu-id="33e85-101">Auswählen einer Gruppe zu analysierender Ressourcen in Arbeitsmappen</span><span class="sxs-lookup"><span data-stu-id="33e85-101">Picking a set of resources to analyze in workbooks</span></span>

<span data-ttu-id="33e85-102">Die Vorlage `Resource Picker` stellt Abonnement-, Ressourcengruppen- und Ressourcenparameter zum Einrichten des Eingabekontexts Ihrer Arbeitsmappe bereit.</span><span class="sxs-lookup"><span data-stu-id="33e85-102">The `Resource Picker` template gets you started with subscription, resource group and resource parameters to set up the input context of your workbook.</span></span> <span data-ttu-id="33e85-103">Mit den Standardparametern werden virtuelle Computer ausgewählt. Sie kann jedoch für einen beliebigen Ressourcentyp konfiguriert werden.</span><span class="sxs-lookup"><span data-stu-id="33e85-103">The default parameters are set to pick virtual machines, but you can configure it to pick any type of resource.</span></span> <span data-ttu-id="33e85-104">Die Vorlage verfügt auch über ein ARG-Abfragesteuerelement, das zeigt, wie Sie die Parameter in Ihren Analysen verwenden.</span><span class="sxs-lookup"><span data-stu-id="33e85-104">The template also has a ARG query control that shows you how to use the parameters in your analyses.</span></span>

![Image](Full.png)

## <a name="setting-up-the-resource-type-to-pick"></a><span data-ttu-id="33e85-106">Einrichten des auszuwählenden Ressourcentyps</span><span class="sxs-lookup"><span data-stu-id="33e85-106">Setting up the resource type to pick</span></span>

1. <span data-ttu-id="33e85-107">Wählen Sie auf der Arbeitsmappen-Symbolleiste die Option `Edit` aus.</span><span class="sxs-lookup"><span data-stu-id="33e85-107">Hit `Edit` on the workbook toolbar.</span></span>
2. <span data-ttu-id="33e85-108">Vor `Subscriptions` wird die Dropdownliste `Resource type` angezeigt:</span><span class="sxs-lookup"><span data-stu-id="33e85-108">You will now be able to see a drop down `Resource type` before `Subscriptions`:</span></span>

    ![Image](Parameter.png)
3. <span data-ttu-id="33e85-110">Erweitern Sie die Dropdownliste, und wählen Sie die gewünschten Ressourcentypen aus.</span><span class="sxs-lookup"><span data-stu-id="33e85-110">Expand the drop down and select the resource types you want picked.</span></span> <span data-ttu-id="33e85-111">Daraufhin werden die Dropdownlisten für Abonnement, Ressourcengruppe und Ressourcen entsprechend aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="33e85-111">This will update the subscription, resource group and resources drop down to match your selection.</span></span>
4. <span data-ttu-id="33e85-112">Klicken Sie rechts unten in der Parametersteuerung auf die Schaltfläche `Edit`.</span><span class="sxs-lookup"><span data-stu-id="33e85-112">Click the `Edit` button at the bottom right of the parameter control.</span></span>
5. <span data-ttu-id="33e85-113">Ändern Sie im Parameterraster in der Zeile `Resources` die Spalte `Display name` von _Virtuelle Computer_ in den Anzeigenamen des ausgewählten Ressourcentyps (beispielsweise _Speicherkonten_).</span><span class="sxs-lookup"><span data-stu-id="33e85-113">In the parameters grid, for the row `Resources`, change the `Display name` column from _Virtual machines_ to friendly name of your selected resource type (e.g. _Storage Accounts_)</span></span>
6. <span data-ttu-id="33e85-114">Klicken Sie auf der Arbeitsmappen-Symbolleiste auf `Done Editing`.</span><span class="sxs-lookup"><span data-stu-id="33e85-114">Click `Done Editing` in the workbooks toolbar.</span></span>

## <a name="selecting-more-or-less-than-10-resources-by-default"></a><span data-ttu-id="33e85-115">Standardmäßiges Auswählen von mehr oder weniger als zehn Ressourcen</span><span class="sxs-lookup"><span data-stu-id="33e85-115">Selecting more or less than 10 resources by default</span></span>

1. <span data-ttu-id="33e85-116">Wählen Sie auf der Arbeitsmappen-Symbolleiste die Option `Edit` aus.</span><span class="sxs-lookup"><span data-stu-id="33e85-116">Hit `Edit` on the workbook toolbar.</span></span>
2. <span data-ttu-id="33e85-117">Klicken Sie rechts unten in der Parametersteuerung auf die Schaltfläche `Edit`.</span><span class="sxs-lookup"><span data-stu-id="33e85-117">Click the `Edit` button at the bottom right of the parameter control.</span></span>
3. <span data-ttu-id="33e85-118">Wählen Sie im Parameterraster die Zeile für `Resources` aus.</span><span class="sxs-lookup"><span data-stu-id="33e85-118">In the parameters grid, select the row for `Resources`</span></span>
4. <span data-ttu-id="33e85-119">Klicken Sie auf der Symbolleiste auf `Edit` (Stiftsymbol).</span><span class="sxs-lookup"><span data-stu-id="33e85-119">Click on the `Edit` (or pencil) icon control toolbar.</span></span>
5. <span data-ttu-id="33e85-120">Scrollen Sie im daraufhin angezeigten Bereich `Edit Parameter` nach unten zum Editor `Azure Resource Graph Query`.</span><span class="sxs-lookup"><span data-stu-id="33e85-120">In the `Edit Parameter` pane that pops up, scroll down to the `Azure Resource Graph Query` editor.</span></span> <span data-ttu-id="33e85-121">Dort sollte sich eine Abfrage wie die folgende befinden:</span><span class="sxs-lookup"><span data-stu-id="33e85-121">It should have a query that looks like this:</span></span>
    ```sql
    Resources
    | where type in~({ResourceTypes})
    | extend resourceGroupId = strcat('/subscriptions/', subscriptionId, '/resourceGroups/', resourceGroup)
    | where resourceGroupId in~({ResourceGroups}) or '*' in~({ResourceGroups})
    | order by name asc
    | extend Rank = row_number()
    | project value = id, label = name, selected = Rank <= 10, group = resourceGroup
    ```
    <span data-ttu-id="33e85-122">Der Code für die Ressourcenauswahl befindet sich in der letzten Zeile der Abfrage: `selected = Rank <= 10`.</span><span class="sxs-lookup"><span data-stu-id="33e85-122">The code for resource selection is in the last line of the query: `selected = Rank <= 10`.</span></span> 

6. <span data-ttu-id="33e85-123">Ändern Sie den Wert von „10“ in einen anderen Wert, um die Standardauswahl zu ändern.</span><span class="sxs-lookup"><span data-stu-id="33e85-123">Change the value from 10 to a different one to change the default selection</span></span>