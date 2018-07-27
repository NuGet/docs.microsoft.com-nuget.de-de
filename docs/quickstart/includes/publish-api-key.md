1. [Melden Sie sich bei Ihrem nuget.org-Konto an](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), oder erstellen Sie ein Konto, wenn Sie noch keines besitzen.

1. Klicken Sie auf Ihren Benutzernamen (oben rechts) und anschließend auf **API Keys** (API-Schlüssel).

1. Wählen Sie **Erstellen**, geben Sie einen Namen für den Schlüssel ein, und wählen Sie **Bereiche auswählen > Push**. Geben Sie unter **API-Schlüssel** für **Globmuster** ein Sternchen (*) ein, und wählen Sie dann **Erstellen**. (Weitere Informationen zu Bereichen finden Sie unten.)

1. Nachdem der Schlüssel erstellt wurde, klicken Sie auf **Copy** (Kopieren), um den Zugriffsschlüssel abzurufen, den Sie in der CLI benötigen:

    ![Kopieren des API-Schlüssels in die Zwischenablage](../media/QS_Create-02-APIKey.png)

1. **Wichtig**: Speichern Sie Ihren Schlüssel an einem sicheren Ort, Sie können den Schlüssel später nicht erneut kopieren. Wenn Sie auf die Seite „API-Schlüssel“ zurückkehren, müssen Sie den Schlüssel erneut generieren, um ihn zu kopieren. Sie können den API-Schlüssel auch entfernen, wenn sie keine Pakete mehr mithilfe von Push über die CLI übertragen möchten.

Mit der Bereichsauswahl können Sie separate API-Schlüssel für verschiedene Zwecke erstellen. Jeder Schlüssel hat seinen Ablaufzeitraum und kann auf bestimmte Pakete (oder Globmuster) festgelegt werden. Jeder Schlüssel ist zudem auf bestimmte Vorgänge begrenzt: Push von neuen Paketen und Updates, Push von ausschließlich Updates oder Entfernen aus Listing. Durch das Festlegen des Gültigkeitsbereichs können Sie API-Schlüssel für verschiedene Personen erstellen, die Pakete für Ihre Organisation so verwalten, dass sie nur über die erforderlichen Berechtigungen verfügen. Weitere Informationen finden Sie in der [Einführung in API-Schlüssel mit begrenztem Gültigkeitsbereich](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html) (blogs.nuget.org).