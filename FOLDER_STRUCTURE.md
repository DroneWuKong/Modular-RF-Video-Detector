# Folder Structure

> **Note:** This is the *planned* layout. Some files marked `(planned)` below
> do not exist yet — this repo is currently a design-phase scaffold containing
> documentation only.

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
│   │   ├── BOM.csv                  # Bill of materials (planned — not yet added)
│   │   └── wiring/
│   │       └── WIRING_DIAGRAM.md    # Pin-by-pin wiring guide (planned — not yet added)
│   │
│   └── addon-58ghz/                 # 5.8 GHz add-on PCB
│       ├── README.md                # Add-on specs + pinout
│       ├── BOM.csv                  # Bill of materials (planned — not yet added)
│       └── wiring/
│           └── WIRING_DIAGRAM.md    # Pin-by-pin wiring guide (planned — not yet added)
│
├── software/
│   ├── README.md                    # Software overview
│   │
│   ├── base/                        # Radxa Zero 3W software
│   │   ├── README.md                # Setup + usage
│   │   ├── setup.sh                 # One-shot setup script (planned — not yet added)
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
│   ├── README.md                    # Print instructions (planned — not yet added)
│   ├── base/                        # Base module enclosure
│   │   └── README.md
│   └── addon/                       # Add-on module enclosure
│       └── README.md
│
└── docs/
    ├── README.md                    # Documentation index
    ├── ARCHITECTURE.md              # Full system architecture
    ├── ASSEMBLY_GUIDE.md            # Step-by-step build guide (planned — not yet added)
    └── WIRING_DIAGRAM.md            # Full system wiring (planned — not yet added)
```

## Quick Navigation

**Building the base unit?**
→ `hardware/base-module/README.md`

**Adding 5.8 GHz module?**
→ `hardware/addon-58ghz/README.md`

**Setting up software?**
→ `software/base/setup.sh` (planned — not yet added)

**Understanding the architecture?**
→ `docs/ARCHITECTURE.md`

**Wiring help?**
→ `hardware/base-module/wiring/WIRING_DIAGRAM.md` (planned — not yet added)
