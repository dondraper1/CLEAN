

[Rainmeter]
Update=1000000
Author=DonDraper1

[Metadata]
Name= CLEAN
Version=1.0
License=Creative Commons Attribution-Non-Commercial-Share Alike 3.0
Information= A Player with Album Artwork, bar and favorite icons. Can change player by changing Player in Variables.

;End of Metadata
;#########################################################
[Variables]

@include=#ROOTCONFIGPATH#Settings.txt

;ENTER YOUR PLAYER NAME HERE
Player=iTunes

;ENTER YOUR RESOLUTION HERE
width=1920

;########################################################
;MEASURES
;########################################################

[mHrs]
Measure=Time
Format=%I

[mM]
Measure=Time
Format=%M

[mAm]
Measure=Time
Format=%p

[mDate]
Measure=Time
Format="%m/%d"

[mVol]
Measure=Plugin
Plugin=Win7AudioPlugin.dll

[mPlayer]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=#Player#
PlayerType=TITLE
DisableLeadingZero=1


[mArtist]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=[mPlayer]
PlayerType=ARTIST

[mAlbum]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=[mPlayer]
PlayerType=ALBUM


[mCover]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=[mPlayer]
PlayerType=COVER
Substitute= "": "default.png"

[mProg]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=[mPlayer]
PlayerType=Progress


[mDur]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=[mPlayer]
PlayerType=DURATION


[mPos]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=[mPlayer]
PlayerType=POSITION


[mRating]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=[mPlayer]
PlayerType=RATING

[mClose]
Measure=Plugin
Plugin=NowPlaying.dll
PlayerName=[mPlayer]
PlayerType=Status
IfEqualValue=0
	IfEqualAction=!Execute[!RainmeterHideMeterGroup Hide Me][!RainmeterHideMeterGroup Text][!RainmeterHideMeterGroup Set][!RainmeterHideMeter Cover][!RainmeterHideMeterGroup Image][!RainmeterHideMeterGroup Button][!RainmeterHideMeterGroup Star][!RainmeterRedraw]
	IfAboveValue=0
	IfAboveAction=!Execute[!RainmeterHideMeterGroup Hide Me][!RainmeterShowMeterGroup Text][!RainmeterShowMeterGroup Set][!RainmeterShowMeter Cover][!RainmeterShowMeterGroup Image][!RainmeterShowMeterGroup Button][!RainmeterShowMeterGroup Star][!RainmeterRedraw]

;########################################################
;METERS
;#######################################################

[Back]
Meter=Image
ImageName=Back.png
x=0
Y=0
W=#width#
H=100
Group=Image

;########################################################
;SONG INFORMATION
;########################################################

[Cover]
Meter=IMAGE
MeasureName=mCover
x=0
y=0
w=100
H=100
SolidColor=FFFFFF10
LeftMouseUpAction=!Execute [!CommandMeasure "mPlayer" "OpenPlayer"]
Group=Image

[PositionText]
Meter=String
MeasureName=mPos
MeasureName2=mDur
X=215
Y=66
FontFace=#font#
FontSize=14
FontColor=#color#
AntiAlias=1
AutoScale=1
StringAlign=Right
Text= "%1/%2"
Group=Text


[Title]
Meter=String
MeasureName=mPlayer
X=120
Y=5
w=480
H=80
ClipString=1
FontFace= #font#
FontSize=32
FontColor=#color#
AntiAlias=1
StringAlign=LeftTop
AutoScale=1
Group=Text

[Artist]
Meter=String
MeasureName=mArtist
X=600
Y=17
W=200
H=30
FontFace= #font#
FontSize=17
StringAlign=Left
ClipString=1
FontColor=#color#
AntiAlias=1
AutoScale=1
Group=Text

[Album]
Meter=String
MeasureName=mAlbum
x=800
Y=r
FontFace=#font#
StringAlign=Left
FontSize=15
FontColor=#color#
AntiAlias=1
AutoScale=1
Group=Text

;################################################################
;BUTTONS
;################################################################

[Prev]
Meter=Image
ImageName=Previous.png
x=500
Y=55
LeftMouseDownAction=!Execute[!RainmeterShowMeter "PreviousBlack"][!RainmeterHideMeter "Previous"][!CommandMeasure "mPlayer" "Previous"][!RainmeterRedraw]
Group=Button

[PreviousBlack]
Meter=Image
ImageName=previousinv.png
x=r
Y=r
LeftMouseUpAction=!Execute [!RainmeterHideMeter "PreviousBlack"][!RainmeterShowMeter "Prev"][!RainmeterRedraw]
Hidden=1
Group=HideMe


[Play]
Meter=Image
ImageName=Play.png
x=35r
Y=-10r
LeftMouseDownAction=!Execute [!RainmeterShowMeter "PlayBlack"][!RainmeterHideMeter "Play"][!RainmeterRedraw][!CommandMeasure "mPlayer" "PlayPause"][!RainmeterRedraw]
Group=Button
GreyScale=1
BackgroundMode=0
Bevel=1

[PlayBlack]
Meter=Image
ImageName=playinv.png
x=r
Y=r
LeftMouseUpAction= !Execute [!RainmeterHideMeter "PlayBlack"][!RainmeterShowMeter "Play"][!RainmeterRedraw]
Hidden=1
Group=HideMe

[Next]
Meter=Image
ImageName=Next.png
X=45r
Y=7r
LeftMouseDownAction=!Execute [!RainmeterShowMeter "NextBlack"][!RainmeterHideMeter "Next"][!CommandMeasure "mPlayer" "Next"][!RainmeterRedraw]
Group=Button

[NextBlack]
Meter=Image
ImageName=nextinv.png
x=r
Y=r
LeftMouseUpAction=!Execute [!RainmeterHideMeter "NextBlack"][!RainmeterShowMeter "Next"][!RainmeterRedraw]
Hidden=1
Group=Hide Me

;######################################################################
;STARS
;######################################################################

[Stars]
Meter=BITMAP
X=680
Y=80
MeasureName=mRating
BitmapImage=Rating.png
BitmapFrames=6
BitmapZeroFrame=1
Group=Star

[1star]
Meter=IMAGE
X=r
Y=r
W=13
H=10
SolidColor=00000001
LeftMouseUpAction=!Execute [!RainmeterPluginBang "mPlayer SetRating 1"]
Group=Star

[2stars]
Meter=IMAGE
X=13r
Y=r
W=13
H=10
SolidColor=00000001
LeftMouseUpAction=!Execute [!RainmeterPluginBang "mPlayer SetRating 2"]
Group=Star

[3stars]
Meter=IMAGE
X=13r
Y=r
W=13
H=10
SolidColor=00000001
LeftMouseUpAction=!Execute [!RainmeterPluginBang "mPlayer SetRating 3"]
Group=Star

[4stars]
Meter=IMAGE
X=13r
Y=r
W=13
H=10
SolidColor=00000001
LeftMouseUpAction=!Execute [!RainmeterPluginBang "mPlayer SetRating 4"]
Group=Star

[5stars]
Meter=IMAGE
X=13r
Y=r
W=13
H=10
SolidColor=00000001
LeftMouseUpAction=!Execute [!RainmeterPluginBang "mPlayer SetRating 5"]
Group=Star

;######################################################################
;PROGRESS BAR
;######################################################################


[BarBack]
Meter=Image
ImageName=barback.png
x=220
Y=59
Group=Image

[Progress]
Meter=Bar
MeasureName=mProg
BarImage=progress.png
x=r
Y=r
BarOrientation=HORIZONTAL
Group=Image

[PercentageText]
Meter=String
MeasureName=mProg
x=337
Y=64
FontFace=#font#
StringStyle=BOLD
FontSize=18
FontColor=#color#
AntiAlias=1
AutoScale=1
PostFix=%
Group=Text


[Prog0]
Meter=IMAGE
SolidColor=0,0,0,1
X=220
Y=59
W=6
H=40
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  0"
Group=Set

[Prog5]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  5"
Group=Set

[Prog10]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  10"
Group=Set

[Prog15]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  15"
Group=Set


[Prog20]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  20"
Group=Set

[Prog25]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  25"
Group=Set

[Prog30]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  30"
Group=Set

[Prog35]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  35"
Group=Set

[Prog40]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  40"
Group=Set

[Prog45]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  45"
Group=Set

[Prog50]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  50"
Group=Set

[Prog55]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  55"
Group=Set

[Prog60]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  60"
Group=Set

[Prog65]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  65"
Group=Set

[Prog70]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  70"
Group=Set

[Prog75]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  75"
Group=Set

[Prog80]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  80"
Group=Set

[Prog85]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  85"
Group=Set

[Prog90]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  90"
Group=Set

[Prog95]
Meter=IMAGE
SolidColor=0,0,0,1
X=12r
Y=r
W=13
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  95"
Group=Set

[Prog100]
Meter=IMAGE
SolidColor=0,0,0,1
X=13r
Y=r
W=12
H=33
LeftMouseDownAction=!CommandMeasure "mPlayer SetPosition  100"
Group=Set


;############################################################
;VOLUME BAR
;############################################################

[VolBarText]
Meter=String
x=940
Y=50
FontFace=#font#
FontSize=15
FontColor=#color#
AntiAlias=1
AutoScale=1
Text=Volume
Group=Text

[VolBarBack]
Meter=Image
ImageName=volbar.png
x=850
Y=75
Group=Image

[VolProgress]
Meter=Bar
MeasureName=mVol
BarImage=volblue.png
x=r
Y=r
BarOrientation=HORIZONTAL
Group=Image



[VolProg0]
Meter=IMAGE
SolidColor=0,0,0,1
X=850
Y=75
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 0"
Group=VolSet

[VolProg5]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 5"
Group=VolSet

[VolProg10]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 10"
Group=VolSet

[VolProg15]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 15"
Group=VolSet


[VolProg20]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 20"
Group=VolSet

[VolProg25]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 25"
Group=VolSet

[VolProg30]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 30"
Group=VolSet

[VolProg35]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 35"
Group=VolSet

[VolProg40]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 40"
Group=VolSet

[VolProg45]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 45"
Group=VolSet

[VolProg50]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 50"
Group=VolSet

[VolProg55]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 55"
Group=VolSet

[Prog60]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 60"
Group=VolSet

[VolProg65]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 65"
Group=VolSet

[VolProg70]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 70"
Group=VolSet

[VolProg75]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 75"
Group=VolSet

[VolProg80]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 80"
Group=VolSet

[VolProg85]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 85"
Group=VolSet

[VolProg90]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 90"
Group=VolSet

[VolProg95]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 95"
Group=VolSet

[VolProg100]
Meter=IMAGE
SolidColor=0,0,0,1
X=10r
Y=r
W=10
H=15
LeftMouseDownAction=!CommandMeasure "mVol SetVolume 100"
Group=VolSet

;############################################################
;CLOCK
;############################################################

[Clock]
Meter=String
MeasureName=mHrs
MeasureName2=mM
MeasureName3=mAM
MeasureName4=mDate
x=(#width#-100)
Y=40
FontSize=16
FontFace=#font#
FontColor=#color#
Text= "%4  %1:%2 %3"
AntiAlias=1
Group=Text
