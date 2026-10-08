Function 1: can_init()
- Inputs: hfdcan1, gpio
- If battery is plugged into the charger (slow_CAN), then set all data to CAN_Charger
- If battery is plugged into the car, then set all data to CAN_CAR
- Reinitialize FDCAN1
- Start FDCAN1
- Open the system for new data
- Return: void

Function 2: HAL_FDCAN_RxFifo0Callback()
- Inputs: hfdcan, RxFifo0ITs
- RxFifo0ITs is the notifications
- If messages aren't empty, if there is an error, print error
- Otherwise, switch statement that goes through messages based on ID (parts of the CAN) and sets data
- Return: void

Function 3: bms_can_faults()
- Inputs: PackData, TotalPack, hfdcan1
- Calculates the total voltage of the battery and finds faults and shows them
- Return: void

Function 4: bms_can_stats()
- Inputs: PackData, TotalPack, hfdcan1
- Calculate min, max, temp, voltage, and total voltage from BMS information
- Send the data and finds faults/errors and shows them
- Return: void

Function 5: bms_can_data()
- Inputs: PackData, TotalPack, hfdcan1, bms_mod_counter, bms_segment_counter
- Convert CAN ID based on bms_mod_counter and bms_segment_counter
- Assign voltages and temperatures with special conversion that offsets number of temp sensors and voltage sensors (calls cell_to_temp_index)
- Checks for end of module and final, fill in rest of the data with 0s
- Check errors and show them
- Return: void

Function 6: bsm_can()
- Inputs: gpio_data, hfdcan1
- Send battery state machine outputs and state
- Return: void

Function 7: bsm_can_ids()
- Inputs: PackData, soc[][CELLS_PER_MOD], pack, hfdcan1
- Send individual BMS board IDs
- Return: void

Function 8: soc_can_stats()
- Inputs: PackData, soc[][CELLS_PER_MOD], pack, hfdcan1
- Gives overall Pack SOC (state of charge) information
- Return: void

Function 9: soc_can_data()
- Inputs: soc[][CELLS_PER_MOD], pack, hfdcan1, soc_mod_counter, soc_segment_counter
- Converting SOC ID based on soc_mod_counter and soc_segment_counter
- Return: void

Function 10: error_can()
- Input: hdfcan1
- Send error messages
- Return: void

Function 11: adc_can()
- Input: adc_data, hdfcan1
- Convert ADCs (Analog to digital converter) and send
- Return: void

Function 12: CAN_SendData()
- Input: id, data, length, hfdcan1
- Sets up the transmit header with the proper ID and length
- Sends all the messages
- Returns a call to function: HAL_FDCAN_AddMessageToTxFifo0(hfdcan1, &txHdr, data)
