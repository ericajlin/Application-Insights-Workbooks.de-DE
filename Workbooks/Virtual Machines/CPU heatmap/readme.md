# <a name="cpu-heatmap"></a>CPU-Wärmebild

Diese Arbeitsmappe bietet eine gute Methode für die Visualisierung von Hotspots in der CPU-Auslastung Ihres virtuellen Computers.

![Anzeigen eines CPU-Wärmebilds](cpu-heatmap.png)

## <a name="changing-the-cpu-threshold"></a>Ändern des CPU-Schwellenwerts
Standardmäßig hebt diese Arbeitsmappe virtuelle Computer mit einem durchschnittlichen `Percentage CPU`-Wert von mehr als 75 % hervor. Wenn dieser Schwellenwert höher oder niedriger sein soll, führen Sie die folgenden Schritte aus:

1. Klicken Sie in der Symbolleiste auf das `Edit`-Element.
2. Klicken Sie im Hive-Steuerelement unten rechts auf die Schaltfläche `↑ Edit`.
3. Scrollen Sie in der Liste `Columns Available After Merge` nach unten, und wählen Sie das `[Added column] - Cell Color`-Element aus.
4. Klicken Sie auf der Symbolleiste der Hive-Steuerelemente auf die Schaltfläche `Edit added item`.
5. Klicken Sie im Bereich, der sich dann öffnet, im Element `Percentage CPU > 75 Result is E8976A` auf `Edit`, um ein Popup mit Einstellungen anzuzeigen.
    1. Legen Sie im Feld `Second operand` den gewünschten Schwellenwert fest, z. B. 90.
        ![Anzeigen eines CPU-Wärmebilds](cpu-heatmap-column-settings.png)
    2. Klicken Sie im Popup auf „Op“.
6. Klicken Sie auf „Speichern und Schließen“.
7. Wählen Sie auf der Arbeitsmappe-Symbolleiste die Option `Done Editing`.
