# Необходимые проверки после обновления с AndroidAPS 2.6

- The program code was changed significantly when switching to AAPS 2.7.
- Therefore it is important that you make some changes or check settings after the update.
- Please see [release notes](Releasenotes-version-2-7-0) for details on new and extended features.

## Проверяем источник ГК

- Check if BG source is correct after update.
- Especially when using [xDrip+](../Configuration/xdrip.md) it might happen, that BG source is changed to Dexcom app (patched).
- Open [Config builder](Config-Builder-bg-source) (hamburger menu on top left side of home screen)
- Scroll down to "BG source".
- Select correct BG source if changes are necessary.

```{image} ../images/ConfBuild_BG.png
:alt: источник ГК
```

## Завершаем экзамен

- AAPS 2.7 contains new objective 11 (in later versions renumbered to objective 10!) for [automation](../Usage/Automation.md).
- You have to finish exam ([objective 3 and 4](Objectives-objective-3-prove-your-knowledge)) in order to complete [objective 11](Objectives-objective-10-automation).
- If for example you did not finish the exam in [objective 3](../Usage/Objectives-objective-3-prove-your-knowledge) yet, you will have to complete the exam before you can start [objective 11](Objectives-objective-10-automation).
- Это не повлияет на другие цели, которые вы уже выполнили. You will keep all finished objectives!

## Установите главный пароль

- Necessary to be able to [export settings](../Usage/ExportImportSettings.md) as they are encrypted as of version 2.7.
- Open Preferences (three-dot-menu on top right of home screen)
- Click triangle below "General"
- Click "Master-Password"
- Enter password, confirm password and click ok.

```{image} ../images/MasterPW.png
:alt: Установить основной пароль
```

## Экспорт настроек

- AAPS 2.7 uses a new encrypted backup format.
- You must [export your settings](../Usage/ExportImportSettings.md) after updating to version 2.7.
- Settings files from previous versions can only be imported in AAPS 2.7. Экспорт будет в новом формате.
- Make sure to store your exported settings not only on your phone but also in at least one safe place (your pc, cloud storage...).
- If you build AAPS 2.7 apk with the same keystore than in previous versions you can install new version without deleting the previous version.
- All settings as well as finished objectives will remain as they were in the previous version.
- In case you have lost your keystore build version 2.7 with new keystore and import settings from previous version as described in the [troubleshooting section](troubleshooting_androidstudio-lost-keystore).

## Autosens (подсказка - не требует действий)

- Autosens is changed to a dynamic switching model which replicates the reference design.
- Autosens will now switch between a 24 and 8 hours window for calculating sensitivity. Он выберет более чувствительный вариант.
- Если пользователи перешли с oref1, они, вероятно, заметят, что система может быть менее динамичной из-за различий в 24 или 8 часах чувствительности.

## Создание пароля для Dana RS (если используется Dana RS)

- Pump password for [Dana RS](../Configuration/DanaRS-Insulin-Pump.md) was not checked in previous versions.
- Open Preferences (three-dot-menu on top right of screen)
- Scroll down and click triangle next to "Dana RS".
- Click "Pump password (v1 only)"
- Enter pump password ([Default password](DanaRS-Insulin-Pump-default-password) is different depending on firmware version) and click OK.

```{image} ../images/DanaRSPW.png
:alt: задать пароль Dana RS
```

To change password on Dana RS follow instructions on [DanaRS page](DanaRS-Insulin-Pump-change-password-on-pump).
