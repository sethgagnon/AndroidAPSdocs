# Obrazovky AndroidAPS

## Hlavní stránka

![Hlavní obrazovka V2.7.](../images/Home2020_Homescreen.png)

Toto je první obrazovka, na kterou narazíte, když spustíte aplikaci AndroidAPS. Obsahuje většinu informací, které budete potřebovat každý den.

### Sekce A – Karty

* Procházejte mezi různými moduly AndroidAPS.
* Obrazovky můžete také změnit tak, že přejedete prstem doleva nebo doprava.
* Displayed tabs can be selected in [config builder](Config-Builder-tab-or-hamburger-menu).

(Screenshots-section-b-profile-target)=

### Sekce B – Profil & cíl

#### Aktuální profil

![Profile switch remaining duration](../images/Home2020_ProfileSwitch.png)

* Aktuální profil je zobrazen v levém panelu.
* Krátkým stiskem panelu profilu zobrazíte detaily profilu
* Long press profile bar to [switch between different profiles](Profiles-profile-switch).
* Pokud byl profil přepnut s dobou trvání, tak se zbývající minuty platnosti profilu zobrazí v závorkách.

#### Cíl

![Temp target remaining duration](../images/Home2020_TT.png)

* Aktuální cílová hladina glykémie je zobrazena v pravém řádku.
* Krátkým stisknutím cílové hodnoty nastavíte [dočasný cíl](../Usage/temptarget.md).
* Pokud je nastaven dočasný cíl, zobrazí se žlutě a zbývající čas v minutách bude zobrazen v závorkách.

(Screenshots-visualization-of-dynamic-target-adjustment)=

#### Vizualizace dynamické úpravy cíle

![Visualization of dynamic target adjustment](../images/Home2020_DynamicTargetAdjustment.png)

* AAPS může dynamicky upravovat vaši cílovou hodnotu na základě citlivosti, pokud používáte algoritmus SMB.
* Enable either one or both of the [following options](Preferences-openaps-smb-settings) 
   * "citlivost zvyšuje cíl" a/nebo 
   * "rezistence snižuje cíl" 
* Jestliže AAPS detekuje rezistenci nebo citlivost, cíl se bude lišit od hodnoty, která je nastavena v profilu. 
* Když tato funkce změní cílovou glykémii, její hodnota bude podbarvena zeleně.

### Sekce C – glykémie a stav smyčky

#### Aktuální hodnota glykémie

* Nejnovější glykémie z CGM je zobrazena na levé straně.
* Color of the BG value reflects the status to the defined [range](Preferences-range-for-visualization). 
   * zelená = v rozmezí
   * červená = pod cílovým rozmezím
   * žlutá = nad cílovým rozmezím
* Šedý blok uprostřed zobrazuje minuty od posledního načtení hodnoty a změny od posledního čtení, za posledních 15 a 40 minut.

(Screenshots-loop-status)=

#### Stav smyčky

![Stav smyčky](../images/Home2020_LoopStatus.png)

* Nová ikona zobrazující stav smyčky:
   
   * zelený kruh = smyčka běží
   * green circle with dotted line = [low glucose suspend (LGS)](Objectives-objective-6-starting-to-close-the-loop-with-low-glucose-suspend)
   * červený kruh = smyčka vypnutá (nefunguje trvale)
   * žlutý kruh = smyčka pozastavena (dočasně pozastavena, ale bude vydán bazální inzulin) - zbývající čas je zobrazen pod ikonou
   * šedý kruh = pumpa odpojena (dočasně žádný výdej inzulínu) - zbývající čas je zobrazen pod ikonou
   * Oranžový kruh = je spuštěn superbolus - zbývající čas je zobrazen pod ikonou
   * modrý kruh s tečkovanou čárou = otevřená smyčka

* Krátkým nebo dlouhým stiskem ikony otevřete dialog smyčky pro přepnutí režimu smyčky (Uzavřená smyčka, Zastavení před nízkou, Otevřená smyčka, Vypnuto), pozastavit / znovu povolit smyčku nebo odpojit / znovu připojit pumpu.
   
   * Pokud krátce stisknete ikonu smyčky, je po výběru některé možnosti v dialogu smyčky vyžadováno ověření
   
   ![Loop status menu](../images/Home2020_Loop_Dialog.png)

(Screenshots-bg-warning-sign)=

#### BG warning sign

Beginning with Android 3.0, you might get a warning signal beneath your BG number on the main screen.

*Note*: Up to 30h hours are taken into accord for AAPS calculations. So even after you solved the origin problem, it can take about 30 hours for the yellow triangle to disappear after the last irregular interval occurred.

To remove it immediately you need to manually delete a couple of entries from the Dexcom/xDrip+ tab.

However, when there are a lot of duplicates, it might be easier to

* [backup your settings](../Usage/ExportImportSettings.md),
* reset your database in the maintenance menu and
* [import your settings](../Usage/ExportImportSettings.md) again

##### Red warning sign: Duplicate BG data

The red warning sign is signaling you to get active immediately: You are receiving duplicate BG data, which does avoid the loop to do its work right. Therefore your loop will be disabled until it is resolved.

![Red BG warning](../images/bg_warn_red.png)

You need to find out why you get duplicate BGs:

* Is Dexcom bridge enabled on your NS site? Disable the bridge by going to heroku (or any other hosting provider), edit the "enable" variable and remove the "bridge" part there. (For heroku [details can be found here](https://nightscout.github.io/troubleshoot/troublehoot/#heroku-settings).)
* Do multiple sources upload your BG to NS? If you use the BYODA app, enable the upload in AAPS but do not enable it in xDrip+, if you use that.
* Do you have any followers that might receive your BG but do also upload it again to your NS site?
* Last resort: In AAPS, go to your NS Client settings, select the sync settings and disable the "Accept CGM data from NS" option.

##### Yellow warning sign

* The yellow warning signal is indicating that your BG arrived in irregular time intervals or some BGs are missing.
   
   ![Yellow BG warning](../images/bg_warn_yellow.png)

* Usually you do not have to take any action. The closed loop will continue to work!

* As a sensor change is interupting the constant flow of BG data a yellow warning sign after sensor change is normal and nothing to worry about.
* Special note for libre users:
   
   * Every single libre slips a minute or two every few hours, meaning you never get a perfect flow of regular BG intervals.
   * Also jumpy readings interrupt the continous flow.
   * Therefore the yellow warning sign will be 'always on' for libre users.

### Sekce D – IOB, COB, BR a AS

![Section D](../images/Home2020_TBR.png)

* Syringe: insulin on board (IOB) - amount of active insulin inside your body
   
   * The insulin on board figure would be zero if just your standard basal was running and there was no insulin remaining from previous boluses. 
   * IOB may be negative if there have recently been periods of reduced basal.
   * Press the icon to see the split of bolus and basal insulin

* Grain: [carbs on board (COB)](../Usage/COB-calculation.md) - yet unabsorbed carbs you have eaten before -> icon pulses if carbs are required

* Purple line: basal rate - icon changes reflecting temporary changes in basal rate (flat at 100%) 
   * Press the icon to see the base basal rate and details of any temp basal (including remaining duration)
* Arrows up & down: indicating actual [autosens](Open-APS-features-autosens) status (enabled or disabled) and value is shown below icon

#### Carbs required

![Carbs required](../images/Home2020_CarbsRequired.png)

* Carbs suggestions are given when the reference design detects that it requires carbs.
* This is when the oref algorithm thinks I can't rescue you by 0 (zero) temping and you will need carbs to fix.
* The carb notifications are much more sophisticated than the bolus calculator ones. You might see carbs suggestion whilst bolus calculator does not show missing carbs.
* Carb required notifications can be pushed to Nightscout if wished, in which case an announcement will be shown and broadcast.

### Sekce E – Stavové indikátory

![Section E](../images/Home2020_StatusLights.png)

* Status lights give a visual warning for 
   * Cannula age
   * Insulin age (days reservoir is used)
   * Reservoir level (units)
   * Sensor age
   * Battery age and level (%)
* If threshold warning is exceeded, values will be shown in yellow.
* If threshold critical is exceeded, values will be shown in red.
* Settings can be made in [preferences](Preferences-status-lights).

(Screenshots-section-f-main-graph)=

### Sekce F – Hlavní graf

![Section F](../images/Home2020_MainGraph.png)

* Graph shows your blood glucose (BG) as read from your glucose monitor (CGM). 
* Notes entered in action tab such as fingerstick calibrations and carbs entries as well as profile switches are shown here. 
* Long press on the graph to change the time scale. You can choose 6, 12, 18 or 24 hours.
* The green area reflects your target range. It can be configured in [preferences](Preferences-range-for-visualization).
* Blue triangles show [SMB](Open-APS-features-super-micro-bolus-smb) - if enabled in [preferences](Preferences-openaps-smb-settings).
* Optional information:
   
   * Predikce
   * Basals
   * Activity - insulin activity curve

#### Activate optional information

* Click the triangle on the right side of the main graph to select which information will be displayed in the main graph.
* For the main graph just the three options above the line "\---\---- Graph 1 \---\----" are available.
   
   ![Main graph setting](../images/Home2020_MainGraphSetting.png)

(Screenshots-prediction-lines)=

#### Prediction lines

* **Orange** line: [COB](../Usage/COB-calculation.md) (colour is used generally to represent COB and carbs)
   
   Prediction line shows where your BG (not where COB itself!) will go based on the current pump settings and assuming that the deviations due carb absorption remain constant. This line only appears if there are known COB.

* **Dark blue** line: IOB (colour is used generally to represent IOB and insulin)
   
   Prediction line shows what would happen under the influence of insulin only. For example if you dialled in some insulin and then didn’t eat any carbs.

* **Light blue** line: zero-temp (predicted BG if temporary basal rate at 0% would be set)
   
   Prediction line shows how the IOB trajectory line would change if the pump stopped all insulin delivery (0% TBR).
   
   *This line appears only when the [SMB](Preferences-advanced-meal-assist-ama-or-super-micro-bolus-smb) algorithm is used.*

* **Dark yellow** line: [UAM](Sensitivity-detection-and-COB-sensitivity-oref1) (un-announced meals)
   
   Unannounced meals means that a significant increase in glucose levels due to meals, adrenaline or other influences is detected. Prediction line is similar to the ORANGE COB line but it assumes that the deviations will taper down at a constant rate (by extending the current rate of reduction).
   
   *This line appears only when the [SMB](Preferences-advanced-meal-assist-ama-or-super-micro-bolus-smb) algorithm is used.*

* **Dark orange** line: aCOB (accelerated carbohydrate absorption)
   
   Similar to COB, but assuming a static 10 mg/dL/5m (-0.555 mmol/l/5m) carb absorption rate. Deprecated and of limited usefulness.
   
   *This line appears only when the older [AMA](Preferences-advanced-meal-assist-ama-or-super-micro-bolus-smb) algorithm is used.*

Usually your real glucose curve ends up in the middle of these lines, or close to the one which makes assumptions that closest resemble your situation.

#### Basals

* A **solid blue** line shows the basal delivery of your pump and reflects the actual delivery over time.
* The **dotted blue** line is what the basal rate would be if there were no temporary basal adjustments (TBRs).
* In times standard basal rate is given the area under the curve is shown in dark blue.
* When the basal rate is temporarily adjusted (increased or decreased) the area under the curve is shown in light blue.

#### Activity

* The **thin yellow** line shows the activity of Insulin. 
* It is based on the expected drop in BG of the insulin in your system if no other factors (like carbs) were present.

### Sekce G – Další grafy

* You can activate up to four additional graphs below the main graph.
* To open settings for additional graphs click the triangle on the right side of the [main graph](Screenshots-section-f-main-graph) and scroll down.

![Additional graph settings](../images/Home2020_AdditionalGraphSetting.png)

* To add an additional graph check the box on the left side of its name (i.e. \---\---- Graph 1 \---\----).

#### Absolute insulin

* Active insulin including boluses **and basal**.

#### Insulin on board

* Shows the insulin you have on board (= active insulin in your body). It includes insulin from bolus and temporary basal (**but excludes basal rates set in your profile**).
* If there were no [SMBs](Open-APS-features-super-micro-bolus-smb), no boluses and no TBR during DIA time this would be zero.
* IOB can be negative if you have no remaining bolus and zero/low temp for a longer time.
* Decaying depends on your [DIA and insulin profile settings](Config-Builder-local-profile). 

#### Carbs On Board

* Shows the carbs you have on board (= active, not yet decayed carbs in your body). 
* Decaying depends on the deviations the algorithm detects. 
* If it detects a higher carb absorption than expected, insulin would be given and this will increase IOB (more or less, depending on your safety settings). 

#### Deviations

* **GREY** bars show a deviation due to carbs. 
* **GREEN** bars show that BG is higher than the algorithm expected it to be. Green bars are used to increase resistance in [Autosens](Open-APS-features-autosens).
* **RED** bars show that BG is lower than the algorithm expected. Red bars are used to increase sensitivity in [Autosens](Open-APS-features-autosens).
* **YELLOW** bars show a deviation due to UAM.
* **BLACK** bars show small deviations not taken into account for sensitivity

#### Sensitivity

* Shows the sensitivity that [Autosens](Open-APS-features-autosens) has detected. 
* Sensitivity is a calculation of sensitivity to insulin as a result of exercise, hormones etc.

#### Activity

* Shows the activity of insulin, calculated by your insulin profile (it's not derivative of IOB). 
* The value is higher for insulin closer to peak time.
* It would mean to be negative when IOB is decreasing. 

#### Deviation slope

* Internal value used in algorithm.

### Section H - Buttons

![Homescreen buttons](../images/Home2020_Buttons.png)

* Buttons for insulin, carbs and Calculator are almost'always on'.
   
   * If connection to pump is lost, the insulin button will not be visible.

* Other Buttons have to be setup in [preferences]Preferences-buttons).

#### Inzulín

![Insulin button](../images/Home2020_ButtonInsulin.png)

* To give a certain amount of insulin without using [bolus calculator](Screenshots-bolus-wizard).
* By checking the box you can automatically start your [eating soon temp target](Preferences-default-temp-targets).
* If you do not want to bolus through pump but record insulin amount (i.e. insulin given by syringe) check the corresponding box.

#### Sacharidy

![Carbs button](../images/Home2020_ButtonCarbs.png)

* To record carbs without bolusing.
* Certain [pre-set temporary targets](Preferences-default-temp-targets) can be set directly by checking the box.
* Time offset: When will you / have you been eaten carbs (in minutes).
* Duration: To be used for ["extended carbs"](../Usage/Extended-Carbs.md)
* You can use the buttons to quickly increase carb amount.
* Notes will be uploaded to Nightscout - depending on your settings for [NS client](Preferences-nsclient).

#### Kalkulačka

* See Bolus Wizard [section below](Screenshots-bolus-wizard)

#### Calibrations

* Sends a calibration to xDrip+ or opens Dexcom calibration dialogue.
* Must be activated in [preferences](Preferences-buttons).

#### CGM

* Opens xDrip+.
* Back button returns to AAPS.
* Must be activated in [preferences](Preferences-buttons).

#### Průvodce rychlým bolusem

* Easily enter amount of carbs and set calculation basics.
* Details are setup in [preferences](Preferences-quick-wizard).

(Screenshots-bolus-wizard)=

## Bolus Wizard

![Bolus wizard](../images/Home2020_BolusWizard_v2.png)

When you want to make a meal bolus this is where you will normally make it from.

### Section I

* BG field is normally already populated with the latest reading from your CGM. If you don't have a working CGM then it will be blank. 
* In the CARBS field you add your estimate of the amount of carbs - or equivalent - that you want to bolus for. 
* The CORR field is if you want to modify the end dosage for some reason.
* The CARB TIME field is for pre-bolusing so you can tell the system that there will be a delay before the carbs are to be expected. You can put a negative number in this field if you are bolusing for past carbs.

(Screenshots-eating-reminder)=

#### Eating reminder

* For carbs in the future the alarm checkbox can be selected (and is by default when a time in the future is entered) so that you can be reminded at a time in the future of when to eat the carbs you have input into AndroidAPS
   
   ![BolusWizard with Eating Reminder](../images/Home2021_BolusWizard_EatingReminder.png)

### Section J

* SUPER BOLUS is where the basal insulin for the next two hours is added to the immediate bolus and a zero TBR is issued for the following two hours to take back the extra insulin. The option only shows when "Enable [superbolus](Preferences-superbolus) in wizard" is set in the [preferences overview](Preferences-overview).
* The idea is to deliver the insulin sooner and hopefully reduce spikes.
* For details visit [diabetesnet.com](https://www.diabetesnet.com/diabetes-technology/blue-skying/super-bolus/).

### Section K

* Shows the calculated bolus. 
* If the amount of insulin on board already exceeds the calculated bolus then it will just display the amount of carbs still required.
* Notes will be uploaded to Nightscout - depending on your settings for [NS client](Preferences-nsclient).

### Section L

* Details of wizard's bolus calculation.
* You can deselect any that you do not want to include but you normally wouldn't want to.
* For safety reasons the **TT box must be ticked manually** if you want the bolus wizard to calculate based on an existing temporary target.

#### Combinations of COB and IOB and what they mean

* For safety reasons IOB boxed cannot be unticked when COB box is ticked as you might run the risk of too much insulin as AAPS is not accounting for what’s already given.
* If you tick COB and IOB unabsorbed carbs that are not already covered with insulin + all insulin that has been delivered as TBR or SMB will be taken into account.
* If you tick IOB without COB, AAPS takes account of already delivered insulin but won’t cover that off against any carbs still to be absorbed. This leads to a 'missing carbs' notice.
* If you bolus for **additional food** shortly after a meal bolus (i.e. additional desert) it can be helpful to **untick all boxes**. This way just the new carbs are being added as the main meal won't necessarily be absorbed so IOB won't match COB accurately shortly after a meal bolus.

(Screenshots-wrong-cob-detection)=

#### Wrong COB detection

![Slow carb absorption](../images/Calculator_SlowCarbAbsorption.png)

* If you see the warning above after using bolus wizard, AndroidAPS has detected that the calculated COB value maybe wrong. 
* So, if you want to bolus again after a previous meal with COB you should be aware of overdosing! 
* For details see the hints on [COB calculation page](COB-calculation-detection-of-wrong-cob-values).

(Screenshots-action-tab)=

## Action tab

![Actions tab](../images/Home2021_Action.png)

### Actions - section M

* Button [profile switch](Profiles-profile-switch) as an alternative to pressing the [current profile](Screenshots-section-b-profile-target) on homescreen.
* Button [temporary target](temptarget-temp-targets) as an alternative to pressing the [current target](Screenshots-section-b-profile-target) on homescreen.
* Button to start or cancel a temporary basal rate. Please note that the button changes from “TEMPBASAL” to “CANCEL x%” when a temporary basal rate is set.
* Even though [extended boluses](Extended-Carbs-extended-bolus-and-why-they-wont-work-in-closed-loop-environment) do not really work in a closed loop environment some people were asking for an option to use extended bolus anyway.
   
   * This option is only available for Dana RS and Insight pumps. 
   * Closed loop will automatically be stopped and switched to open loop mode for the time running extended bolus.
   * Make sure to read the [details](../Usage/Extended-Carbs.md) before using this option.

(Screenshots-careportal-section-n)=

### Careportal - section N

* Displays information on
   
   * sensor age & level (battery percentage)
   * insulin age & level (units)
   * cannula age
   * pump battery age & level (percentage

* Less information will be shown if [low resolution skin](Preferences-skin) is used.

(Screenshots-sensor-level-battery)=

#### Sensor level (battery)

* Needs xDrip+ nightly build Dec. 10, 2020 or newer.
* Works for CGM with additional transmitter such as MiaoMiao 2. (Technically sensor has to send cat level information to xDrip+.)
* Thresholds can be set in [preferences](Preferences-status-lights).
* If sensor level is the same as phone battery level you xDrip+ version is probably too old and needs an update.
   
   ![Sensor levels equals phone battery level](../images/Home2021_ActionSensorBat.png)

### Careportal - section O

* BG check, prime/fill, sensor insert and pump battery change are the base for the data displayed in [section N](Screenshots-careportal-section-n).
* Prime/Fill allows you to record pump site and insulin cartridge change.
* Section O reflects the Nightscout careportal. So exercise, announcement and question are special forms of notes.

### Tools - section P

#### History Browser

* Allows you to ride back in AAPS history.

#### CDD

* Total daily dose = bolus + basal per day
* Some doctors use - especially for new pumpers - a basal-bolus-ratio of 50:50. 
* Therefore ratio is calculated as TDD / 2 * TBB (Total base basal = sum of basal rate within 24 hours). 
* Others prefer range of 32% to 37% of TDD for TBB. 
* Like most of these rules-of-thumb it is of limited real validity. Note: Your diabetes may vary!

![Histroy browser + TDD](../images/Home2021_Action_HB_TDD.png)

(Screenshots-insulin-profile))=

## Inzulínový profil

![Inzulínový profil](../images/Screenshot_insulin_profile.png)

* This shows the activity profile of the insulin you have chosen in [config builder](Config-Builder-insulin). 
* The PURPLE line shows how much insulin remains after it has been injected as it decays with time and the BLUE line shows how active it is.
* The important thing to note is that the decay has a long tail. 
* If you have been used to manual pumping you have probably been used to assuming that insulin decays over about 3.5 hours. 
* However, when you are looping the long tail matters as the calculations are far more precise and these small amounts add up when they are subjected to the recursive calculations in the AndroidAPS algorithm.

For a more detailed discussion of the different types of insulin, their activity profiles and why all this matters you can read an article here on [Understanding the New IOB Curves Based on Exponential Activity Curves](https://openaps.readthedocs.io/en/latest/docs/While%20You%20Wait%20For%20Gear/understanding-insulin-on-board-calculations.html#understanding-the-new-iob-curves-based-on-exponential-activity-curves)

And you can read an excellent blog article about it here: [Why we are regularly wrong in the duration of insulin action (DIA) times we use, and why it matters…](https://www.diabettech.com/insulin/why-we-are-regularly-wrong-in-the-duration-of-insulin-action-dia-times-we-use-and-why-it-matters/)

And even more at: [Exponential Insulin Curves + Fiasp](https://seemycgm.com/2017/10/21/exponential-insulin-curves-fiasp/)

## Stav pumpy

![Stav pumpy](../images/Screenshot_PumpStatus.png)

* Different information on pump status. Displayed information depends on your pump model.
* See [pumps page](../Hardware/pumps.md) for details.

## Péče

Careportal replicated the functions you will find on your Nightscout screen under the “+” symbol which allows you to add notes to your records.

### Review carb calculation

![Review carb calculation on t tab](../images/Screenshots_TreatCalc.png)

* If you have used the [Bolus Wizard](Screenshots-bolus-wizard) to calculate insulin dosage you can review this calculation later on ts tab.
* Just press the green Calc link. (Depending on pump used insulin and carbs can also be shown in one single line in ts.)

(Screenshots-carb-correction)=

### Korekce sacharidy

![Treatment in 1 or 2 lines](../images/Treatment_1or2_lines.png)

Treatment tab can be used to correct faulty carb entries (i.e. you over- or underestimated carbs).

1. Zkontrolujte a zapamatujte si aktuální COB a IOB na domovské obrazovce.
2. V závislosti na pumpě se mohou sacharidy v záložce ošetření zobrazovat společně s inzulínem v jednom řádku nebo jako samostatný záznam (např. s Danou RS).
3. Odstraňte záznam s chybným množstvím sacharidů.
4. Ujistěte se, že sacharidy byly úspěšně odstraněny kontrolou COB na domovské obrazovce.
5. Kontrolu proveďte také pro IOB, pokud v záložce ošetření jeden řádek obsahuje sacharidy i inzulín.
   
   -> Nejsou-li sacharidy odstraněny tak, jak bylo zamýšleno, a přidáte další sacharidy, jak je zde vysvětleno (6.), COB budou příliš vysoké a to může vést k podání příliš vysokého množství inzulínu.

6. Zadejte správné množství sacharidů pomocí tlačítka na domovské obrazovce a ujistěte se, že jste nastavili správný čas události.

7. Pokud je v záložce ošetření pouze jedna řádka obsahující sacharidy i inzulín, musíte také přidat množství inzulínu. Nezapomeňte nastavit správný čas události a po potvrzení nového záznamu zkontrolujte IOB na domovské obrazovce.

## Loop, AMA / SMB

* These tabs show details about the algorithm's calculations and why AAPS acts the way it does.
* Calculations are each time the system gets a fresh reading from the CGM.
* For more details see [APS section on config builder page](Config-Builder-aps).

## Profil

![Profil](../images/Screenshots_Profile.png)

* Profile contains information on your individual diabetes settings:
   
   * DIA (Duration of Insulin Action)
   * IC or I:C: Insulin to Carb ratio
   * ISF: Insulin Sensitivity Factor
   * Basal rate
   * Target: Blood glucose level that you want AAPS to be aiming for

* As of version 3.0 only [local profile](Config-Builder-local-profile) is possible. The local profile can be edited on your smartphone and synced to your Nightscout site.

(Screenshots-treatment)=

## Bolus

History of the following treatments:

* Bolus & carbs -> option to [remove entries](Screenshots-carb-correction) to correct history
* [Prodloužený bolus](Extended-Carbs-extended-bolus-and-switch-to-open-loop-dana-and-insight-pump-only)
* Temporary basal rate
* [Temporary target](../Usage/temptarget.md)
* [Přepínání profilu](../Usage/Profiles.md)
* [Careportal](CPbefore26-careportal-discontinued) - notes entered through action tab and notes in dialogues

## BG Source - xDrip+, BYODA...

![BG Source tab - here xDrip](../images/Screenshots_BGSource.png)

* Depending on your BG source settings this tab is named differently.
* Shows history of CGM readings and offers option to remove reading in case of failure (i.e. compression low).

## NSClient

![NSClient](../images/Screenshots_NSClient.png)

* Displays status of the connection with your Nightscout site.
* Settings are made in [preferences](Preferences-nsclient). You can open the corresponding section by clicking the cog wheel on the top right side of the screen.
* For troubleshooting see this [page](../Usage/Troubleshooting-NSClient.md).