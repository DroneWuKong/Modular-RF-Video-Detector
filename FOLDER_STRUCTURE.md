# Folder Structure

```
Modular-RF-Video-Detector/
│
├── README.md                        # Project overview (START HERE)
├── FOLDER_STRUCTURE.md              # This file
│
├── hardware/
│   ├── README.md                    # Hardware overview
│   │
│   ├── base-module/                 # Radxa Zero 3W base PCB
│   │   ├── README.md                # Base module specs + pinout
│   │   ├── BOM.csv                  # Bill of materials
│   │   └── wiring/
│   │       └── WIRING_DIAGRAM.md    # Pin-by-pin wiring guide
│   │
│   └── addon-58ghz/                 # 5.8 GHz add-on PCB
│       ├── README.md                # Add-on specs + pinout
│       ├── BOM.csv                  # Bill of materials
│       └── wiring/
│           └── WIRING_DIAGRAM.md    # Pin-by-pin wiring guide
│
├── software/
│   ├── README.md                    # Software overview
│   │
│   ├── base/                        # Radxa Zero 3W software
│   │   ├── README.md                # Setup + usage
│   │   ├── setup.sh                 # One-shot setup script
│   │   ├── scanner/                 # RF + WiFi scanning daemon
│   │   │   └── README.md
│   │   └── web/                     # Web UI + video streaming
│   │       └── README.md
│   │
│   └── addon-58ghz/                 # 5.8 GHz add-on software
│       ├── README.md                # Setup + usage
│       └── scanner/                 # RTL8812AU + RX5808 scanner
│           └── README.md
│
├── case-3d/
│   ├── README.md                    # Print instructions
│   ├── base/                        # Base module enclosure
│   │   └── README.md
│   └── addon/                       # Add-on module enclosure
│       └── README.md
│
└── docs/
    ├── README.md                    # Documentation index
    ├── ARCHITECTURE.md              # Full system architecture
    ├── ASSEMBLY_GUIDE.md            # Step-by-step build guide
    └── WIRING_DIAGRAM.md            # Full system wiring
```

## Quick Navigation

**Building the base unit?**
→ `hardware/base-module/README.md`

**Adding 5.8 GHz module?**
→ `hardware/addon-58ghz/README.md`

**Setting up software?**
→ `software/base/setup.sh`

**Understanding the architecture?**
→ `docs/ARCHITECTURE.md`

**Wiring help?**
→ `hardware/base-module/wiring/WIRING_DIAGRAM.md`
