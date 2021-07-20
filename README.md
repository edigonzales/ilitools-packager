# ilitools-packager

## Todo
- Dateiablage? HTTP? FTP? S3?
- Warum funktionieren DMG von Github Action nicht?
- Falls App-Name Punkte beinhaltet, wird die Anwendung (auf macOS only?) nicht gestartet.
- jdeps auf Apple Silicon funktioniert nicht. 

## Building

```
jdeps --class-path 'libs/*' --multi-release base -recursive --ignore-missing-deps --print-module-deps ilivalidator-1.11.10.jar
jlink --add-modules java.base,java.desktop,java.management,java.sql --output ilivalidator-jre
jpackage --icon icon-ilivalidator-128x128.icns --name ilivalidator --type dmg --input libs --main-jar ilivalidator-1.11.10.jar --main-class org.interlis2.validator.Main -d output --runtime-image ilivalidator-jre --app-version 1.11.10 --java-options -Xmx2g
```

- jdeps: Eruiert die Abhängigkeiten der Anwendung von der JRE. 
- jlink: Erzeugt auf Basis der Abhängigkeiten eine möglichst kleine JRE.
- jpackage: Herstellen des OS-spezifischen Packages mit der eigenen JRE.