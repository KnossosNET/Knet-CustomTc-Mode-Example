# Knet Single Tc Mode Example
This example is divided into two modes, portable mode and normal mode.
<br />
<br />
**Portable mode** is where you place a "kn_portable" folder next to the launcher .exe and all files will be stored inside of it, Knet data folder, customisation files, library data, and FSO pilots and settings files. This is what you normally would want for single TC mode.
<br />
**Normal mode** you will place the "custom_launcher.json" file next to launcher executable and all data folders still works in a similar way to how you normally use the launcher. The only diference being that Knossos data folder instead of being "%appdata%\KnossosNET" it will be "%appdata%\KnossosNET\{MODID}" to avoid conflicts.
In this mode to set the library path, the user will be asked to select a install folder on the Home View.
<br />
<br />
<br />
**Features:**
- Optional Custom FSO Data folder for pilots and FSO settings
- Disabling Launcher Updates
- Background image and starting window size
- Disabling some menu entries
- Additional Custom CMD for FSO
- Disable log file
- Disabling nebula services
- Configurable html content on Home View
- Configurable link buttons on Home View
- Optional additional menu content using HTML
<br />
<br />
**Customisations options for custom_launcher.json:**
<br />
```csharp
        /// <summary>
        /// If left empty Knet will try to pick up the "custom_launcher.json" file.
        /// Change it to a mod id to hardcode SingleTC ON using the default settings se there.
        /// </summary>
        public static string? ModID { get; private set; } = null;

        /// <summary>
        /// If enabled, the FSO data folder will changed to use the ModID instead "FreeSpaceOpen"
        /// This gives this TC its own settings and pilot saving location.
        /// </summary>
        public static bool UseCustomFSODataFolder { get; private set; } = true;

        /// <summary>
        /// This allows Knet to search for launcher updates (or not) at the start.
        /// Disabling it will completely disable launcher updates.
        /// If you are forking this and want to provide your own repo to check for updates
        /// change "GitHubUpdateRepoURL" in Knossos.cs
        /// </summary>
        public static bool AllowLauncherUpdates { get; private set; } = true;

        /// <summary>
        /// Custom title for the launcher window. It is recommended to add the mod name to it
        /// Launcher version is auto-added at the end
        /// </summary>
        public static string WindowTitle { get; private set; } = "Knet Launcher";

        /// <summary>
        /// Starting width size of the launcher window
        /// This is also the min width
        /// null for auto
        /// </summary>
        public static int? WindowWidth { get; private set; } = 1024;

        /// <summary>
        /// Starting height size of the launcher window
        /// This is also the min height
        /// null for auto
        /// </summary>
        public static int? WindowHeight { get; private set; } = 540;

        /// <summary>
        /// The first time the user opens the launcher, the main menu should be expanded or collapsed?
        /// After that it will use the saved state
        /// </summary>
        public static bool MenuOpenFirstTime { get; private set; } = false;

        /// <summary>
        /// Add the regular FSO engine view to the menu
        /// </summary>
        public static bool MenuDisplayEngineEntry { get; private set; } = true;

        /// <summary>
        /// Add the regular Knet debug view to the menu
        /// </summary>
        public static bool MenuDisplayDebugEntry { get; private set; } = true;

        /// <summary>
        /// Add the regular Knet Nebula Login view to the menu
        /// This is intended to allow nebula user creation and login
        /// To download private versions of the TC, normally you do not want this
        /// buts its there as an option
        /// </summary>
        public static bool MenuDisplayNebulaLoginEntry { get; private set; } = false;

        /// <summary>
        /// Display the regular Knossos community menu item
        /// </summary>
        public static bool MenuDisplayCommunityEntry { get; private set; } = false;

        /// <summary>
        /// Display the regular Knossos settings menu item
        /// If you do this you may want to add "-no_ingame_options" to the custom cmdline
        /// </summary>
        public static bool MenuDisplayGlobalSettingsEntry { get; private set; } = false;

        /// <summary>
        /// Add custom buttons to the menu
        /// </summary>
        public static CustomMenuButton[]? CustomMenuButtons { get; private set; }

        /// <summary>
        /// Yet another cmdline option, pass it as a string array. 
        /// It has the lowest priority, same options can be overriden by mod cmdline.
        /// </summary>
        public static string[]? CustomCmdlineArray { get; private set; }

        /// <summary>
        /// Disabling this disconnects the launcher from Nebula completely. Meaning.
        /// It can not install, update or modify installations. And it cant do api calls and will not get repo_minimal.json
        /// It is only good to provide static game files not meant to be changed or be updated by a 3rd party app or service
        /// </summary>
        public static bool UseNebulaServices { get; private set; } = true;

        /// <summary>
        /// Whatever to write or not the Knossos.log file to the datafolder, disabling it will prevent this file from be written.
        /// But the output to the debug console will still be there if you use it.
        /// </summary>
        public static bool WriteLogFile { get; private set; } = true;

        /// <summary>
        /// Path to the background image for the home view
        /// It is recommended this image to be about 200px less in width than the starting WindowWidth
        /// Supports local image in the Knet data folder, a local full path, harcoded image or remote https:// URL
        /// Supports APNGs, GIF, PNG and JPG
        /// Examples:
        /// Harcoded Image:
        /// "avares://Knossos.NET/Assets/fs2_res/kn_screen_0.jpg"
        /// Data Folder image (same path to were the repo_minimal.json is downloaded for the current running mode):
        /// "GgqNPDqW0AAMR80.png"
        /// Remote Image (will be cached locally):
        /// "https://video-meta.humix.com/poster/h2YKfXkqITvJ/pKvBUijWRO2_IChwVu.jpg"
        /// </summary>
        public static string? HomeBackgroundImage { get; private set; } = "avares://Knossos.NET/Assets/general/custom_home_background.jpg";

        /// <summary>
        /// Set a path to the welcome HTML message on home screen
        /// Uses the same path rules as HomeBackgroundImage
        /// null to disable or put a path to a empty file if you want to display it at some point
        /// </summary>
        public static string? HomeWelcomeHtml { get; private set; } = null;

        /// <summary>
        /// Thickness string to use as margin for the WelcomeHTML display
        /// left, up, right, down
        /// </summary>
        public static string? HomeWelcomeMargin { get; private set; } = "50,50,50,0";

        /// <summary>
        /// Optional Link buttons that are displayed in the home screen that
        /// if clicked opens a external web link in user browser
        /// Icon path follows the same rules as HomeBackgroundImage, so URL, embedded and local images are supported.
        /// </summary>
        public static LinkButton[]? HomeLinkButtons { get; private set; }
```

<br />

**The HTML Renderer is not a browser**
<br />
The HTML renderer is very basic and only be able to do, maybe, HTML4 stuff. Dosent support JS, animated images videos and some stylization things.