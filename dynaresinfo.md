How timings are calculated

dynares.c

The provided content includes licensing information, headers, and some variable declarations. To understand how the resolution is calculated, we need to look for specific functions or logic related to resolution calculation. Let's extract more content from the file and search for key terms such as "resolution," "width," "height," "calculate," or similar terms. This will help us identify the relevant section of the code.

Let's continue to extract more content and look for the logic that calculates the resolution.

From the extracted content, we can identify a few functions that interact with resolution variables and handle specific aspects of resolution and rotation:

1. **`dynares_is_mame_rotated`**: This function checks if the system is running MAME and if the rotation is set to certain values. It returns a boolean indicating if MAME is rotated.
   
2. **`dynares_check_rotation`**: This function checks the rotation of the system and swaps the width and height if necessary based on the rotation.

3. **`dynares_video_show_info`**: This function displays video information including resolution, interlacing mode, and refresh rate (Hz).

4. **`dynares_init`**: This function initializes various settings related to resolution, CRT type, and other parameters.

Let's focus on the `dynares_init` function to see if it provides more details on how the resolution is calculated or initialized. We'll extract more content starting from where this function is defined.

The `dynares_init` function initializes the resolution based on various settings and conditions. Here is a summary of the relevant parts of the function:

1. **Initial Settings**:
   - `sys_name`, `rotation`, `base_width`, and `base_height` are initialized from the system and settings.
   - `dynares_check_rotation` is called to adjust width and height if necessary based on rotation.

2. **Native Mode**:
   - If `dynares` is set to "native", the function sets the screen width and height to the base values.
   - For specific systems (DOS, GBA, NGP, X68K, GBC), the function adjusts the width and height to appropriate values. For example:
     - DOS systems with 640x400 resolution are adjusted to 640x480.
     - GBA with 240x160 resolution can be adjusted to 720x480 or 256x224 depending on `handheld_full` setting.
     - NGP with 160x152 resolution can be adjusted to 480x456 or 256x224 based on `handheld_full`.
     - GBC with 160x144 resolution is adjusted to 256x224.

3. **Viewport and Font Size**:
   - The viewport width and height are set to the adjusted resolution values.
   - The font size is adjusted based on the height of the resolution. For example:
     - If the height is less than or equal to 300, the font size is set to 6.
     - If the height is greater than 300, the font size is set to 12.

To understand how the timing is calculated in the code, we need to look for functions or sections related to timing calculations. These sections might involve variables like `timing`, `srtiming`, `sys_timing`, `gam_timing`, and any relevant logic for calculating or adjusting timing parameters.

Let's extract more content from the file to find functions or logic related to timing calculations. We'll search for keywords such as "timing," "calculate," "fps," "region," or similar terms that could indicate timing-related operations.

The extracted content continues to show adjustments for screen width and height based on different modes and system types, but it doesn't yet reveal the logic specifically for timing calculations.

Let's search within the file content for functions or code blocks that involve timing variables such as `timing`, `srtiming`, `sys_timing`, `gam_timing`, and any other timing-related operations. We will continue extracting more content to find the relevant sections.

The extracted content continues to focus on different modes (`superx`, `fixed`, `custom`) and their respective adjustments for resolution, viewport, and font size. However, towards the end, it starts mentioning `sr_init`, `sr_set_log_level`, and `sr_set_monitor`, which are likely related to timing initialization and configuration.

Let's extract more content to delve deeper into the `sr_init` and other related functions that handle timing calculations. This should give us a clearer picture of how the timing is managed in the code.

The newly extracted content provides more details about how the timing is calculated and managed in the code. Here is a summary of the relevant sections:

1. **Initialization and Configuration**:
   - `sr_init()`, `sr_set_log_level(0)`, `sr_set_monitor(crt_type)`, and other functions are called to initialize and configure the timing system.
   - `sr_set_interlace_force_even(1)` and `sr_set_v_shift_correct(0)` are used to set specific timing parameters.

2. **User Mode and Timing Retrieval**:
   - Depending on the `crt_type`, the user mode is set with `sr_set_user_mode()`. For example:
     - For "arcade_31" CRT type, the user mode is set to 640x480 at 60 Hz.
     - For other CRT types, the user mode is set to 320x240 at 60 Hz.
   - `sr_init_disp("auto")` initializes the display settings automatically.
   - `sr_get_timing()` retrieves the timing parameters for the specified width, height, refresh rate, and CRT type, and stores them in the `srtiming` structure.

3. **Formatting and Logging Timing Information**:
   - `snprintf()` is used to format the timing information into the `sys_timing` string.
   - `sr_deinit()` deinitializes the timing system after the system timing is generated.
   - The process is repeated to generate the game timing based on the current width, height, and frames per second (fps).

4. **Game Timing Calculation**:
   - The game timing is calculated similarly to the system timing, using `sr_get_timing()` and formatting the results into the `gam_timing` string.
   - The timing information is logged with `RARCH_LOG()`.

The timing calculation involves initializing the timing system, setting specific parameters based on the CRT type and desired resolution, and retrieving detailed timing parameters using `sr_get_timing()`. These parameters are then formatted and logged for use in the application.



switchres_wrapper.cpp

The file switchres_wrapper.cpp contains the implementation of the SwitchRes C wrapper API, which is used for modeline generation for emulation. The functions in this file are part of the API that interacts with the sr_get_timing function. Here is a summary of the relevant sections from the provided content:

Initialization and Configuration:

sr_init(): Initializes the SwitchRes manager and parses the configuration from switchres.ini.
sr_load_ini(char* config): Loads and parses the specified configuration file, updating the display settings.
Display Initialization:

sr_init_disp(const char* scr): Sets the screen and adds the display. Initializes the display and returns 1 if successful, otherwise 0.
Deinitialization:

sr_deinit(): Deletes the SwitchRes manager, cleaning up resources.
Monitor and Mode Settings:

sr_set_monitor(const char* preset): Sets the monitor preset.
sr_set_interlace_force_even(int value): Sets whether to force even interlacing.
sr_set_v_shift_correct(int value): Sets the vertical shift correction value.
sr_set_user_mode(int width, int height, int refresh): Sets the user mode with the specified width, height, and refresh rate.
Mode Conversion:

disp_best_mode_to_sr_mode(display_manager* disp, sr_mode* srm): Converts the best display mode to SwitchRes mode, setting various parameters like width, height, refresh rate, scaling, and interlacing.
To find the specific implementation of sr_get_timing, let's extract more content from the file to locate this function and understand its logic. ​​

The implementation of the sr_get_timing function is partially visible. Here's an explanation of the visible part and a continuation to understand the full logic:

Function Signature and Logging:

The function sr_get_timing takes parameters for width, height, refresh rate, CRT type, interlace flag, and a pointer to a timing structure.
It logs the input parameters for debugging purposes.
Display Manager:

The function retrieves the display manager instance from the SwitchRes manager (swr->display()).
If the display manager is nullptr, it logs an error and returns 0.
Mode Retrieval:

The function attempts to get a modeline for the specified width, height, refresh rate, and interlace flag using disp->get_mode().
If the modeline is nullptr, it logs an error indicating that the mode is not supported and returns -1.
Let's extract the next part of the content to see the complete implementation of sr_get_timing and understand how the timing parameters are filled into the timing structure. ​​

The implementation of the sr_get_timing function continues with the following steps:

Mode Verification:

It checks if the display has successfully obtained a mode using disp->got_mode().
Logs the obtained mode details including width, height, refresh rate, and mode type.
Position Adjustments:

The function sets screen position adjustments (h_pos and v_pos) based on the width and refresh rate.
These adjustments help in fine-tuning the horizontal and vertical positions of the display.
Modeline Values:

Retrieves modeline values such as hactive, hbegin, hend, htotal, vactive, vbegin, vend, vtotal, and hfreq from the return_mode.
Computes pixel_freq as the product of htotal and hfreq.
Retrieves interlace, hsync, and vsync values.
Timing Values:

Sets the horizontal and vertical synchronization polarities.
Modifies the horizontal position by adjusting the hhi and hhf values equally to shift the picture left or right.
Let's extract more content to see the complete implementation and understand how the timing structure is populated. ​​

The complete implementation of the sr_get_timing function is now visible. Here is a detailed explanation of the logic used to calculate the timing:

Screen Position Adjustments:

h_pos and v_pos are adjusted based on the width and refresh rate to fine-tune the display position.
These adjustments shift the horizontal and vertical positions of the display.
Retrieving Modeline Values:

Horizontal and vertical values are retrieved from the return_mode:
hhh, hhi, hhf, hht: Horizontal active pixels, beginning, end, and total.
vvv, vvi, vvf, vvt: Vertical active pixels, beginning, end, and total.
pixel_freq: Calculated as the product of hht and hfreq.
interlaced, hsync, vsync: Interlace and synchronization polarities.
Position and Size Adjustments:

Horizontal and vertical positions (hhi, hhf, vvi, vvf) are adjusted by h_pos and v_pos.
Horizontal total (h_total), front porch (h_f_porch), and back porch (h_b_porch) are calculated.
Vertical total (v_total), front porch (v_f_porch), and back porch (v_b_porch) are calculated.
Frames per second (fps) is calculated as pixel_freq / (hht * vvt).
Even Porch Values:

Forces even values for horizontal front and back porches.
Populating the timing Structure:

The timing values are set in the return_timing structure:
hhh, hsync, h_f_porch, h_b_porch, h_total
vvv, vsync, v_f_porch, v_b_porch, v_total
vsync_offset_a, vsync_offset_b, pixel_rep, fps
interlaced, pixel_freq, aspect
Return Value:

Returns 1 on success, or 0 if there is an error adding the mode.
This function meticulously calculates and adjusts various timing parameters to ensure proper display settings based on the input resolution and refresh rate.
