## gta.dat

The gta*.dat file lists which files define the game map. It can be found in the game's data directory, and is known as gta3.dat in Grand Theft Auto III, gta_vc.dat in Grand Theft Auto: Vice City, and simply gta.dat in Grand Theft Auto: San Andreas. The same file format is also used for the default.dat file in the same directory.

## Format
The files are in plain text format so they can be opened with any text editor (like Notepad). Line comments are indicated by the character # (number sign) and empty lines are allowed. They can be placed anywhere in the file. Since there are different types of files, a keyword is needed for each entry. Most entries use the following format, where the path is relative to the game's base directory:

<keyword> <path>

Although the file itself is not split up into sections, entries are usually grouped by type and arranged in a special order according to the game's loading sequence:

Keyword | Games | Description | Example
------- | ----- | ----------- | -------
CDIMAGE | <img src="http://aux.iconspalace.com/uploads/gta-iii-icon-128.png" width="16" height= "16"><img src="https://steamuserimages-a.akamaihd.net/ugc/884253767815809101/E12B2FBA58134B56A8B7D046F5109390D1C06F2C/" width="16" height= "16"> | Links to additional IMG archives (other than the hardcoded ones). In GTA San Andreas, a maximum of five entries are supported; any more will crash the game. CDIMAGE is supported in GTA III and GTA Vice City but it is unused in the default data files. | CDIMAGE MODELS\EXAMPLE.IMG
IMG | <img src="https://www.gtainside.com/downloads/picr/2017-08/1503174392_gta_sa.jpg" width="16" height= "16"><img src="http://files.softicons.com/download/game-icons/gta-iv-icons-by-th3-prophetman/ico/IV.ico" width="16" height= "16"> | | IMG MODELS\EXAMPLE.IMG
IMGLIST | <img src="http://files.softicons.com/download/game-icons/gta-iv-icons-by-th3-prophetman/ico/IV.ico" width="16" height= "16"> | Links to external image list files. | IMGLIST common:/DATA/EXAMPLE.TXT
WATER | <img src="http://files.softicons.com/download/game-icons/gta-iv-icons-by-th3-prophetman/ico/IV.ico" width="16" height= "16"> | Links to external water plane placement files. The identifier can hold more than one parameter. It is unconfirmed either this also works for other identifiers. | WATER /DATA/EXAMPLE1.DAT
IDE | <img src="http://aux.iconspalace.com/uploads/gta-iii-icon-128.png" width="16" height= "16"><img src="https://steamuserimages-a.akamaihd.net/ugc/884253767815809101/E12B2FBA58134B56A8B7D046F5109390D1C06F2C/" width="16" height= "16"><img src="https://www.gtainside.com/downloads/picr/2017-08/1503174392_gta_sa.jpg" width="16" height= "16"><img src="http://files.softicons.com/download/game-icons/gta-iv-icons-by-th3-prophetman/ico/IV.ico" width="16" height= "16"> | Links to item definition files. | IDE DATA\MAPS\EXAMPLE.IDE

COLFILE 	GTA III GTA Vice City GTA San Andreas 	Links to collision files. An additional parameter between keyword and path associates the file to a level. If this is 0, the col file is used by the whole map; a higher number (1 to 3) assigns it to one of the level. 	

COLFILE 0 MODELS\COLL\EXAMPLE.COL

MAPZONE 	GTA III 	Links to zone files. 	

MAPZONE DATA\EXAMPLE.ZON

IPL 	GTA III GTA Vice City GTA San Andreas 	Links to IPL-style item placement and zone files. 	

IPL DATA\EXAMPLE.ZON
IPL DATA\MAPS\EXAMPLE.IPL

TEXDICTION 	GTA III GTA Vice City GTA San Andreas 	Links to external texture dictionaries. 	

TEXDICTION MODELS\EXAMPLE.TXD

MODELFILE 	GTA III GTA Vice City GTA San Andreas 	Links to external model files. 	

MODELFILE MODELS\GENERIC\EXAMPLE.DFF

SPLASH 	GTA III GTA Vice City GTA San Andreas 	Links to splash screens that appear when transitioning between levels. The argument for these is not a path, but just the name (without extension) of a texture dictionary in the \models\txd directory. Might be ignored, though. 	

SPLASH loadsc2

HIERFILE 	GTA III GTA Vice City GTA San Andreas 	Unknown purpose. 	
EXIT 	GTA III GTA Vice City GTA San Andreas 	Stops any further processing of the file. 	

Since Grand Theft Auto IV has various subdirectories which need to be identified there are new identifiers at the start of the path. They identify the exact location relative to the executeable file. Those are:

platform:
common:

Internally they will be replaced with the internal directory description and appendet to the installation directory of the game. Example:

platform:/DATA/MAPS/MANHAT/MANHAT12.IPL 

gets

PC/DATA/MAPS/MANHAT/MANHAT12.IPL 

which finally is transformed to (e.g.)

C:\Program Files\Rockstar Games\Grand Theft Auto 4\PC\DATA\MAPS\MANHAT\MANHAT12.IPL
