-------------------------------------
Min 4 Image Viewer
-------------------------------------

	Image viewer program for Linux running X-Desktop enviroment.
	Single window for fast and convenient view and browse, with acurate zoom and pan features.
	Key and mouse navigation customizable trough command line interface
	or configuration file.
	Internally uses Imlib2 library, so can load any image formats that 
	Imlib2 understands. This includes: JPEG, PNG, GIF, BMP and more.


Build Requirements
---------------------------

	Following libraries are needed and should be installed 
	as developement versions on the system:
	
		* Imlib2
		* dl
		* X11
		* pthread

Build Instructions
--------------------------

	* Unpack downloaded archive file.
	* Navigate to a subdirectory "./projects/01_cli".
	* Make sure it contains "makefile" file.
	* Use command "make release" to compile and build.
	* If successful, binary file will be created in
	  "./projects/01_cli/bin/release" subdirectory


Command Line Interface
-----------------------------------

	min4iv --filelist FILE [OPTIONS]
	
	min4iv --file_in_dir FILE [OPTIONS]
	
	min4iv [OPTIONS] file1 file2 file3 ... fileN


OPTIONS
--------------

	--filelist FILE

		Text file that contains files to browse, one file per line.
		Additionally, one or more of individual files can be specified
		at command line.

	--start_at FILE

		File name to start browsing at. For use toogether with the
		'--filelist' option. If not used, then by default, first file
		in the list is used to start the browsing at.

	--file_in_dir FILE

		File to open at startup, and also, a directory with image
		files that will be added to the list automatically.
		The other option, '--start_at', should not be used with this one.

	--help

		Show this help and exit.

	--sort_mode alpha|natsort|none  --  default: alpha

		Initial list sorting mode.
		All input files will be sorted if method specified is
		different than 'none'.
		Sorting is done on UTF-8 strings only.
		In alphanumerical sorting, 'alpha', comparision is
		case-insensitive while case is considered only for english
		characters.

	--initial_metrics fit|center|center2  --  default: fit

		How to position newly loaded images.
		By default image may be resized to fit inside 
		the windpw.

	--zoom_step FLOAT  --  default: 1.17

		Floating point value used when zoommin-in or out.
		Eg. value 1.2 causes bigger scalling steps than value 1.1.

	--pidfile FILE

		Name of file that is created and contains PID of
		the process.

	--bg COLOR

		Background color. 6 hex digit format, only.
		Eg. AA8080 or FF00FF.

	--bg_fs COLOR

		Same as '--bg' option but for use only when in full-screen mode,
		when there is no title bar or task manager visible.
		Eg. on many X-Desktop window managers, window can be switched into
		full-screen using the F11 key.

	--wmax

		Maximize on startup.

	--wmax2 FLOAT/EDGE

		Pseudo maximize on startup.
		Float value is the amout of how much to make the window smaller.
		Value marked as EDGE tells form which window side to subtract
		the size from. EDGE must be set to 'L', 'R', 'T' or 'B'.
		While window can be maximized with the '--wmax' switch instead, this one
		is provided as an alternative, potentially smoother way.
		Eg. '--wmax2 0.1/B' makes window 'maximized' but with the height set to 
		90 percent instead, leaving some space below the window not covered.

	--bShowDbg

		Print more info to stdout.

	--bDontRotate 0|1   --   default: 0

		Do not go to the first image file on the list end.

	--geometry WxH[+X+Y]
	--g WxH[+X+Y]

		Window Geometry on startup.
		X and Y can be both set to 'C', special value,
		to cause centering on the screen.

	--high_prio CHARACTERS

		For use when sorting in alpha-numerical mode, ie. when '--sort_mode' is
		set to 'alpha'.
		ASCII Characters that are considered the highest priority.
		Eg. including character tilde ('~' (0x7E)) in this list, will sort
		this character with highest priority, before letters,
		numbers, and even before 0x01.
		Characters in the list, priority between themself, is determined
		by their order.

	--low_prio CHARACTERS

		Same as '--high_prio' option, but this is to cause placement
		at the end of the list, after any other character.
		Characters can be specified percent-encoded, under condition
		that the last character is itself percent-encoded.
		Eg. set the last character to '%00' to have it itself ignored,
		but actually, percent-decode the other characters.

	--bShowActions

		Shows action names and exits.
		These are names that can be used when binding action to keys
		or buttons.

	--bind_k KEY=ACTION

		Binds key or button to an action.
		Eg. to make the delete key quit the program use 'Delete=Quit'
		KEY can also be specified as HEX value with 0x prefix,
		eg. '0xffbe' (F1 in this case) (This is an Xlib feature).

	--bNoDefaultBinds 0|1   --   default: 0

		Do not assign any default binds.
		This switch must appear before any actual user bind made via
		the '--bind_k' switch.

	--bShowBinds 0|1   --   default: 1

		Shows all key binds in the program on startup. Includes
		any default binds.

	--nMoveByKeyAmount NUMBER    --    default: 16

		How much to move when using keyboard, in sigle button press.

	--config_file FILE

		Configuration file that contains command line options.
		Each line should contain option name followed by value. Simple parsing.
		Example file contents:
			--bg_fs FF88FF
			--bind_k Delete=Quit
			--bind_k c=Quit
		Each line must begin with correct option name, that starts with
		double dash, followed by space character. Only after that space
		character the string can be quoted.
		If file names are to be specified, that potentially contain space
		characters, the line must start with a double dash ('--'), followed 
		by space, then followed by quoted file name.


	Notes About Binding Actions
	---------------------------
		The action 'MousePanButton' can only be bound to a mouse button,
		M1, M2, M3, and so forth. Eg. 'M1=MousePanButton'


