

# J1939 Standard DBC Database

A collection of high-accuracy CAN database (.dbc) files for the SAE J1939 protocol. This database is designed for developers working with heavy-duty vehicle telematics, engine control units (ECUs), and automotive diagnostics.

## Technical Specifications
- **Protocol:** SAE J1939
- **Identifier Format:** 29-bit Extended
- **Bit Timing:** Optimized for standard J1939 data rates (250/500 kbps)
- **Compatibility:** Vector CANdb++, Busmaster, PCAN-Explorer, SavvyCAN

## Parameter Groups Defined
The database includes definitions for the following critical PGNs:

- **PGN 61444 (EEC1):** Engine Speed, Torque Mode, and Percent Torque
- **PGN 61443 (EEC2):** Accelerator Pedal Position and Switch Status
- **PGN 65265 (CCVS1):** Wheel-Based Vehicle Speed
- **PGN 65254 (TD):** Real-time Clock, Date, and Time
- **PGN 65257 (LFI):** Trip and Total Fuel Consumption
- **PGN 65263 (EFL_P1):** Engine Oil Pressure, Coolant Level, and Crankcase Pressure
- **PGN 65269 (AMB):** Ambient Air and Road Surface Temperatures
- **PGN 0:** Proprietary Control High Resolution Torque

## Features
- **Accurate SPN Mapping:** Includes Signal-to-SPN attribute mapping for tool-specific filtering.
- **Value Tables:** Integrated bit-field definitions for status signals (e.g., Error, Not Available, Active).
- **Proper Scaling:** Resolution and offset values are derived from SAE J1939-71 standards.

## Usage
1. Download the `J1939_Core_Signals.dbc` file.
2. Import the file into your preferred CAN analyzer or simulation tool.
3. Use the defined signals to decode raw CAN traffic into human-readable physical values.

# DBC File Structure Explained

## Overview

A **DBC (CAN Database)** file is a text file that describes how to decode CAN bus messages. It acts as a "dictionary" that translates raw CAN bytes into meaningful engineering values like engine speed, temperature, or vehicle speed.

---

## Complete DBC File Structure

```dbc
VERSION ""

NS_ : 
    NS_DESC_
    CM_
    BA_DEF_
    BA_
    VAL_
    CAT_DEF_
    CAT_
    FILTER
    BA_DEF_DEF_
    EV_DATA_
    ENVVAR_DATA_
    SGTYPE_
    SGTYPE_VAL_
    BA_DEF_SGTYPE_
    BA_SGTYPE_
    SIG_TYPE_REF_
    VAL_TABLE_
    SIG_GROUP_
    SIG_VALTYPE_
    SIGTYPE_VALTYPE_
    BO_TX_BU_
    BA_DEF_REL_
    BA_REL_
    BA_DEF_DEF_REL_
    BU_SG_REL_
    BU_EV_REL_
    BU_BO_REL_
    SG_MUL_VAL_

BS_:

BU_:

BO_ 61444 EEC1: 8 Vector__XXX
 SG_ EngineSpeed : 32|16@1+ (0.125,0) [0|8031.875] "rpm" Vector__XXX

CM_ BO_ 61444 "Electronic Engine Controller 1";

BA_DEF_ SG_  "SPN" INT 0 524287;
BA_DEF_ BO_  "VFrameFormat" ENUM  "StandardCAN","ExtendedCAN","reserved","J1939PG";

BA_DEF_DEF_  "SPN" 0;
BA_DEF_DEF_  "VFrameFormat" "J1939PG";

BA_ "VFrameFormat" BO_ 61444 3;
BA_ "SPN" SG_ 61444 EngineSpeed 190;

VAL_ 61444 EngineTorqueMode 0 "No request" 15 "Not available";
