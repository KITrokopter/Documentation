# Common data types

-- none --

# API


## Systemstart und Systemshutdown

*   Name: System
*   Sender: API
*   Empfänger: Alle außer API
*   Beschreibung: Kanal, in dem die API den Modulen den Start- und Beende-befehl geben kann.

### Daten

```
Header header
uint8 command # 1 = Start, 2 = Ende
```

## Nachrichten

*   Name: Message
*   Typ: Topic
*   Sender: Alle außer API
*   Empfänger: API
*   Beschreibung: Kanal, über den Nachrichten in die API gesendet werden können.

### Daten

```
Header header
uint32 senderID
uint8 type # 1 = Message, 2 = Warning, 3 = Error
string message
```

## Anmeldeservice

*   Name: announce
*   Sender: Alle außer API // Die API hat per default den Namen API
*   Empfänger: API
*   Beschreibung: Service an dem sich jede Anwendung anmeldet.

### Daten

```
Header header
uint8 type # 0 = Camera, 1 = Quadcopter, 2 = Controller, 3 = Position
uint64 cameraId # Wenn type != 0 dann cameraId undefiniert
string initializeServiceName
---
uint32 ID # Wenn ID = -1 Dann Fehler
```

# Steueranwendung

## Gesetzte Formation

*   Name: SetFormation
*   Typ: Topic
*   Sender: API
*   Empfänger: Steuerungsanwendung
*   Beschreibung: Topic mit dem die API die vom User gesetzte Formation weitergeben kann.

### Daten

```
Header header
int16 distance
int16 amount
float64[] xPositions
float64[] yPositions
float64[] zPositions
```

## Bewege Formation

*   Name: MoveFormation
*   Typ: Topic
*   Sender: API
*   Empfänger: Steuerungsanwendung
*   Beschreibung: Service mit dem die API die vom User gesetzte Formation weitergeben kann.

### Daten

```
Header header
float64 xMovement
float64 yMovement
float64 zMovement
```

## Bewegung der Quadrokopter

*   Name: quadcopter_movement_{id}
*   Typ: Topic
*   Sender: Steuerungsanwendung
*   Empfänger: Quadkopteranwendung
*   Beschreibung: Bewegungsbefehle (roll, pitch, yaw, thrust) and Quadkopter.

### Daten

```
Header header
uint16 thrust
float32 roll
float32 pitch
float32 yaw
```

## Starte Kalibrierung

*   Name: StartCalibration
*   Typ: Service
*   Sender: API
*   Empfänger: Steuerungsanwendung
*   Beschreibung: Service mit dem die API den Kalibrierungsprozess starten kann.

### Daten

```
Header header
uint32 chessboardWidth # The amount of horizontal corners of the chessboard.
uint32 chessboardHeight # The amount of vertical corners of the chessboard.
float64 chessboardRealWidth # The width of one chessboard field.
float64 chessboardRealHeight # The height of one chessboard field.
---
bool ok
```

## Mache Kalibrierungsbild

*   Name: TakeCalibrationPicture
*   Typ: Service
*   Sender: API
*   Empfänger: Steuerungsanwendung
*   Beschreibung: Service, der bewirkt, dass alle Kameras ein Bild machen, und wenn genug gute Bilder dabei sind, werden diese an die API gesendet.
*   Requires: Image defined in sensor_msgs

### Daten

```
Header header
---
sensor_msgs/Image[] images
uint32[] ids # The ids of the cameras that belong to the images.
```

## Berechne Kalibrierung

*   Name: CalculateCalibration
*   Typ: Service
*   Sender: API
*   Empfänger: Steuerungsanwendung
*   Beschreibung: Service, der die Kalibrierung berechnet.

### Daten

```
Header header
---
float64[] cameraXPositions
float64[] cameraYPositions
float64[] cameraZPositions
float64[] cameraRotationMatrices # Contains the 3x3 rotation matrices for the cameras.
                                 # Every matrix has 9 entries row by row.
uint32[] IDs
```

## Aktuelle Positionen der Quadrokopter

*   Name: quadcopter_position_{id}
*   Typ: Topic
*   Sender: Steueranwendung
*   Empfänger: API
*   Beschreibung: Aktuelle Positionen der Quadrokopter für die API

Daten:
```
Header header
float64 x
float64 y
float64 z
```

## Steuerungsdaten für Quadrokopter

*   Name: CurrentPositions
*   Sender: Steueranwendung
*   Empfänger: Quadcopters
*   Beschreibung: Kanal um die Bewegungsdaten der Quadrokopter zu senden

Daten
```
Header header
uint32 quadcopterdId
uint16 thrust
float32 xPosition
float32 yPosition
float32 zPosition
float32 roll
float32 pitch
float32 yaw
```

# Kameraanwendung

## Bilder

*   Name: Picture
*   Typ: Topic
*   Sender: Kameraanwendung
*   Empfänger: API-Anwendung
*   Beschreibung: Kanal um Bilder zu senden

### Daten

```
Header header
uint32 ID
uint32 imageNumber # Bei Kalibrierung Nummer des Kalibrierungs-
# bilds, sonst inkrementiert pro Bild
bool calibrationImage # True if image is used for calibration of single camera.
uint64 timestamp # Wann das Bild gemacht wurde
uint8[640*480*3] image, BGR format, 1 byte per channel.
```
## Positionsinformationen

*   Name: RawPosition
*   Typ: Topic
*   Sender: Kameraanwendung
*   Empfänger: Positionsmodul
*   Beschreibung: Kanal um die Positionsinformationen die aus dem Bild extrahiert wurden zu senden.

### Daten

```
Header header
uint32 ID
uint64 timestamp # Wann das Quellbild gemacht wurde
float64 xPosition
float64 yPosition
uint32 quadcopterId
```
## Bildsendungsaktivierung

*   Name: PictureSendingActivation
*   Typ: Topic
*   Sender: API
*   Empfänger: Kameraanwendung
*   Beschreibung: Kanal um das Senden der Bilder zu aktivieren und deaktivieren.

### Daten

```
Header header
uint32 ID # if 0, all cameras should be activated/deactivated.
bool active
```

## Kalibrierungsauftrag

*   Name: CalibrateCamera
*   Typ: Topic
*   Sender: API
*   Empfänger: Kameraanwendung
*   Beschreibung: Kanal um das Kalibrieren einer Kamera zu starten. Kalibrierungsbilder werden über das Bildertopic gesendet. Bei Erfolg werden die Daten über das Einzelkamera-Kalibrierungsdatentopic gesendet.

### Daten

```
Header header
uint32 ID
uint32 imageAmount
uint32 imageDelay
uint32 boardWidth
uint32 boardHeight
float32 boardRectangleWidth
float32 boardRectangleHeight
```
## Einzelkamera-Kalibrierungsdaten

*   Name: CameraCalibrationData
*   Typ: Topic
*   Sender: API, Kameraanwendung
*   Empfänger: API, Kameraanwendung
*   Beschreibung: Kanal zum Senden von Kalibrierungsdaten

### Daten

```
Header header
# uint64 cameraHardwareId # We don't have that right now...
uint32 ID
bool createdByCamera
float64[3*3] intrinsics
float64[4] distortion
```

## Initialisierung der Kamera

*   Name: InitializeCameraService[ID]
*   Typ: Service
*   Sender: API
*   Empfänger: Kameraanwendung
*   Beschreibung: Kanal zum Initialisieren der Kamera

### Daten

```
Header header
uint32[] hsvColorRanges # erster Range: [0-1], zweiter Range: [2-3] …
uint32[] quadCopterIds # erster Copter: [0], zweiter Copter: [1] …
---
uint8 error # 0 bei ok, != 0 sonst
```

# Quadrokopteranwendung

## Quadrokopter Statusinformationen

*   Name: quadcopter_status_{ID}
*   Message-Typ: quadcopter_status.msg
*   Typ: Topic
*   Sender: Quadrokopteranwendung
*   Empfänger: API-Anwendung
*   Beschreibung: Topic, an welches die Quadrokopteranwendung periodisch neue Statusinformationen der Quadrokopter schickt.

### Daten

```
Header header
float32 battery_status
float32 link_quality
uint16 motor_m1
uint16 motor_m2
uint16 motor_m3
uint16 motor_m4
float32 stabilizer_roll
float32 stabilizer_pitch
float32 stabilizer_yaw
uint16 stabilizer_thrust
```

## Search quadcopters

* name: search_link_{ID}
* service type: search_links.srv
* type: service
* sender: quadcopter application
* receiver: api application
* description: service, which searches for all available quadcopters and returns their channels

### data

```
---
uint8[] channels
```
