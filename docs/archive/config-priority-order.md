### <a name="priority-ordering"></a>Sortieren nach Priorität

Womöglich hilft es Ihnen, wenn Sie über die „Prioritätsreihenfolge“ nachdenken, in der Einstellungen angewendet werden. Diese stellt im Grunde das Gegenteil der Verarbeitungsreihenfolge dar. Wenn sich ein Projekt z.B. am Speicherort `c:\A\B\C` befindet, wendet NuGet Einstellungen in der folgenden Prioritätsreihenfolge an, d.h. Einstellungen, die in der Reihenfolge eine höhere Priorität erhalten haben, werden zuerst angewendet:

    (For solution-level packages only in NuGet 2.x; ignored in NuGet 3.x)
    c:\A\B\C\.nuget\NuGet.Config

    (For all version of NuGet)
    c:\A\B\C\NuGet.Config
    c:\A\B\NuGet.Config
    c:\A\NuGet.Config
    c:\NuGet.Config

    configFile, if specified

    (Ignored in NuGet 3.4 and later if -configFile is used)
    %AppData%\NuGet\NuGet.Config

    (NuGet 2.6 to 3.5)
    %ProgramData%\NuGet\Config\{IDE}\{Version}\{SKU}\NuGet.Config
    %ProgramData%\NuGet\Config\{IDE}\{Version}\NuGet.Config
    %ProgramData%\NuGet\Config\{IDE}\NuGet.Config
    %ProgramData%\NuGet\Config\NuGet.Config

    (NuGet 4.0+)
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\{Version}\{SKU}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\{Version}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\{IDE}\NuGet.Config
    %ProgramFiles(x86)%\NuGet\Config\NuGet.Config