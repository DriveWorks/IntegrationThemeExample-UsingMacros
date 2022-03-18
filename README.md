# DriveWorks Live - Integration Theme Example - Using Macros
### Version: 1.0.0
#### Minimum DriveWorks Version: 18.0

A distributable example that demonstrates running Macros using the Integration Theme.

---

Please note: DriveWorks are not accepting pull requests for this example.  
Join our [online community](https://my.driveworks.co.uk) for discussion, resources and to suggest other examples.

---

### In this example:

`index.html`
- Creates a new Specification.
- Renders a DriveWorks Form (optional)
    - Used to visually demonstrate change when running Macros, but not required.
- Runs the configured Macro (`config.js`) when clicking the custom `<button>`.

`advanced.html`
- Creates a new Specification.
- Renders a DriveWorks Form (optional)
    - Used to visually demonstrate change when running Macros, but not required.
- Runs the following configured Macros when clicking the corresponding custom `<button>`:
    - Specification Macro (`runMacro`)
        - Triggers configured Macro (`config.macroName`)
        - Passes pre-configured custom Macro Argument (`My Argument`) and Caller (`Custom Site Button`)
    - Control Macro (`runControlMacro`)
        - Triggers configured Macro (`config.macroName`) on pre-named Control (`ControlName`)
        - The argument set on the Control will be used.
        - Update this pre-filled value to target a different Control.
    - Touch Point Macro (`runTouchPointMacro`)
        - Triggers Macro set to pre-configured Node (`Root\\NodeName`) on pre-named Control (`PreviewControlName`)
        - Update these pre-filled values to target a different Control and/or Node.

### To use:
1. Clone this repository, or download as a .zip

2. In `DriveWorksLiveConfigUser.xml`, ensure a Group Alias for a Group containing Macros is present e.g. `name="UsingMacros"`.
    * See [Integration Theme Connection Settings](https://docs.driveworkspro.com/Topic/IntegrationThemeSettings#Connection-Settings) for additional guidance.

3. To allow Macros to be triggered using the Web API, ensure they are exposed via `DriveWorksConfigUser.xml`.
    * A single Macro can be exposed like so:
        ```
        <connections>
            <sharedGroupAlias OR individualGroupAlias ...>
                <permissions>
                    <project name="MyProjectName">
                        <macro name="MyMacroName">
                            <team name="Administrators"/>
                        </constant>
                    </project>
                </permissions>
            </sharedGroupAlias OR /individualGroupAlias>
        </connections>
        ```
    * For further help, see [Integration Theme Permission Settings](https://docs.driveworkspro.com/Topic/IntegrationThemeSettings#Permissions).

4. Enter your Integration Theme details into `config.js`.
    * `serverUrl` - The URL that hosts your Integration Theme, including any ports.
    * `groupAlias` - The public alias created for the Group containing the DriveApps to render (as configured in `DriveWorksConfigUser.xml`).
        * This *must* be specified for each Group you wish to use.
        * This allows you to mask the true Group name publicly, if desired.
        * See [Integration Theme Connection Settings](https://docs.driveworkspro.com/Topic/IntegrationThemeSettings#Connection-Settings) for additional guidance.
    * `projectName` - The name of the Project to render a Specification from.
        * These is pre-filled with the supplied Project's name, but can be changed if required.
    * `macroName` - The name of the Macro to run when the custom buttons are clicked (as exposed by `DriveWorksConfigUser.xml`).

5. Ensure that the Integration Theme server is running, using any of the available methods (e.g. Personal Web Edition, DriveWorks Live, IIS)
    * For more information, see [Selecting the Integration Theme](https://docs.driveworkspro.com/Topic/IntegrationThemeSelect).

6. Open the example HTML files locally (localhost) or on a remote server.
    * Ensure `<corsOrigins>` in DriveWorksConfigUser.xml permits requests from this location.
    * See [Integration Theme Configuration Settings](https://docs.driveworkspro.com/Topic/IntegrationThemeSettings#Configuration-Settings) for additional guidance.

7. Click the various `<button>` elements to trigger the configured Macros inside the Specification.

8. If encountering any issues, check the browser's console for error messages (F12)

### Potential Issues:
* When serving this example for a domain different to your DriveWorks Live server, e.g. api.my-site.com from company.com, 'SameSite' cookie warnings may be thrown when the Client SDK attempts to store the current session id.
    * This appears as "Error: 401 Unauthorized" in the browser console, even with the correct configuration set. 
    * To resolve:
        * Ensure you are running DriveWorks 18.2 or above, HTTPS is enabled in DriveWorks Live's settings and a valid SSL certificate has been configured via DriveWorksConfigUser.xml.
        * See [Integration Theme Settings](https://docs.driveworkspro.com/Topic/IntegrationThemeSettings) for additional guidance.

---

This source code has been made available to demonstrate how you can integrate with DriveWorks using the DriveWorks Live API.
This code is provided under the MIT license. For more details, see the included LICENSE file.

The example requires that you have the latest DriveWorks Live SDK installed, operational and remotely accessible.
