# Week 2: Hardware

<!-- insert Table of Contents here -->

## The Modern Computer

*"You can't understand infrastructure until you understand hardware."*

### Intro to Computer Hardware

#### What are ports?
**Ports** are connection points that we can connect devices to that extend the functionality of our computer.

#### What is a CPU?
- The **CPU (Central Processing Unit)** is the brain of our computer, it does all the calculations and data processing.

- **RAM (Random Access Memory)** is our computer's short-term memory.

- **Hard drive** holds all of our data, which includes all of our music, pictures, and applications.

- **Motherboard** is the body or circulatory system of the computer that connects all the pieces together. 

- **Power supply** converts electricity from the wall outlet into a format the computer can use.

### Programs and Hardware

#### What is a program?
- **Programs** are instructions that tell the computer what to do.

- **External Data Bus** is an internal network of wires, which send voltage to wires to represent on (1) or off (0)

- **Registers** store the data the CPU works with.

- **Memory Controller Chip (MCC)** is a bridge between the CPU and the RAM, like a nerve in your brain controlling thoughts or memories.

- **Address Bus** connects the CPU to the MCC, and sends the *location* of the data, but not the data itself. Then, the MCC looks for the data in the hard drive, then sends it to the CPU via the EDB. 

- **Cache** is smaller than RAM, but can store more frequently-used data in a way that's easier and faster to use. 

- **Clock wire** lets the CPU know it can start doing calculations. This is triggered by voltage sent to the clock wire, and is referred to as a *clock cycle*.

- **Clock speed** is the maximum number of clock cycles that the computer can handle in a certain time period (measured in Hz).

- **Overclocking** increases the rate of a CPU's clock cycles to increase performance. This technique has advantages and disadvantages.

## Components

### CPU

- The most important part of the computer.

- **Instruction set** is a list of instructions the CPU can run (hard-coded, differing by manufacturer, not unlike a car engine).

- You need to make sure a CPU is compatible with a motherboard. Make sure the CPU and motherboards' sockets and pins match.
  - LGA and PGA sockets

- A **heat sink** pulls heat from the CPU and dissipates it with a fan or other medium.

### RAM

- Computer's short-term memory.

- The data is volatile--once you power off your machine, the data stored in RAM is cleared.

- RAM defined by the amount of data it can process at once (for example, 16 GB worth of programs).

- The most common type of RAM is DRAM, or **dynamic random-access memory**.
  - Other types of memory sticks using DRAM chips include **dual inline memory module (DIMM)** sticks, which feature different pin sizes.
  - **Synchronous DRAM (SDRAM)** synchronizes to the computer's clock speed, which lets it process data faster.
  - **Double data rate SDRAM (DDR SDRAM/DDR)** is faster and more efficient than previous versions.
    - DDR 4 is currently the fastest type of short-term memory for your computer.

### Motherboards

- Can expand computer functionality through expansion cards, routes power from the power supply, and allows parts of the computer to communicate with each other.

- **Chipset** decides how components talk to each other in the computer.
  - **Northbridge** connects RAM and video cards
  - **Southbridge** maintains I/O (input/output) controllers, like hard drives and USB devices that input and output data.

- The chipset allows you to manage data between the CPU, RAM, and peripherals.

- **Peripherals** are external devices we connect to our computer, like a mouse, keyboard, and monitor.

- **Expansion slots** give us the ability to increase the functionality of a computer.

- The standard for expansion bus today is the **Peripheral Component Interconnect (PCI) Express**.

- The most common form factor for motherboards is **Advanced Technology eXtended (ATX**
  - **Information Technology eXtended* is a smaller version (mini, nano, pico varieties exist).

### Storage

- HDD and SSD
  - RPM

#### ATA Drives
- [Supplemental reading](https://www.techwalla.com/articles/difference-between-ata-and-sata-hard-drives)

- SATA is the most common

- NVM Express (or NVMe)
  - [Cisco: NVMe for Absolute Beginners](https://blogs.cisco.com/datacenter/nvme-for-absolute-beginners)
  - [Supplemental reading](https://searchstorage.techtarget.com/definition/NVMe-non-volatile-memory-express)

- "Hot-swappable"

### Power Supplies

- Computers use AC voltage, and **power supplies** converts AC from the wall to low-voltage DC power to use in the computer.

- **Amperage** measured in amps; amps pull electricity as needed, whereas voltage pushes all electricity.

- **Wattage** is the amount of volts and amps that a device needs.

- You can power most basic desktops with a 500W power supply.

- It's better to err on the side of larger power supplies.

- Knowing how to diagnose power issues is a critical skill for IT support specialists.

### Mobile Devices

- Mobile devices are computers too, featuring CPUs, RAM, storage, power systems, and peripherals.
  - The difference is they're portable and powered by batteries.

- Mobile devices' components are usually integrated, and not interchangeable.
  - **System on a Chip (SoC)** packs the CPU, RAM, and sometimes even the storage onto a single chip. 
    - Used by very small mobile devices.
    - Advantage is small size and less battery power use.

- Mobile devices can use peripherals and can *be* peripherals.

- Mobile devices can use standard or proprietary ports/connectors, requiring specific adapters or connectors.

#### Standard power, data, display, and connector types 
 - USB-C
 - Lightning adapter
 - Mini USB
 - Micro USB
 - Micro HDMI
 - Mini HDMI
 - Mini display port 

- IT professionals may be called upon to help users with mobile devices, including:
  - Setup
  - Troubleshooting
  - Repairs
  - Replacement

### Batteries and Charging Systems

- Mobile devices use rechargeable batteries.
  - May use a external charger, cradle, stand, or wireless charger.

- Rechargeable batteries have a limited lifespan, measured in **charge cycles**. 
  - A **charge cycle** is one full charge and discharge of a battery.

- Charging circuit manages the power transfer from external power source to rechargeable battery, similar to a power supply unit (PSU), in regards to input power compared to output power.

- Mismatching chargers to devices can damage the battery, device, and the charger.

- Batteries should be charged or discharged in their **safe operating temperature** range. 
    - Otherwise they risk swelling, rupturing, or catching on fire.

- Always ensure the charger, battery, and device are all designed to work with each other.

### Peripherals

- **Peripherals** Anything that you connect to your computer externally that adds functionality.

- **USB** stands for **Universal Serial Bus** and is the most popular connection type.
  - You'll most commonly run into:
    - USB 2.0 (transfer speeds of 480 Mb/s)
    - USB 3.0 (transfer speeds of 5 Gb/s)
    - USB 3.1 (transfer speeds of 10 Gb/s)

#### Don't mistake transfer speeds
- Mb != MB
  - MB is **megabyte**, or **unit of data storage**
  - Mb/s is a **megabit per second**, which is a **unit of data transfer rate**.
    - Example: To transfer a 1MB file in a second, you'll need an 8 Mb/s connection speed (because there are **8 bits** in **1 byte**)
    - Just use simple multiplication. :)

#### USB ports

- USB ports are backwards-compatible
- USB A can charge devices

- In general:
  - USB 2.0 (black)
  - USB 3.0 (blue)
  - USB 3.1 (teal)

- Most recent is **Type-C connector**, becoming a universal standard for display and data transfer, and intended to replace many peripheral connection types.

- Other input standards include:
  - **DVI** and **VGA**, which only output video
  - **HDMI** a standard in televisions and computers, outputting both audio and video
  - **DisplayPort** also outputs audio and video
  - **USB Type C** can handle data transfer and power, on top of audio and video.

#### Useful links for connecting displays
 - [Windows](https://support.microsoft.com/help/27911/windows-10-connect-to-a-projector-or-pc)
 - [MacOS](https://support.apple.com/guide/mac-help/mchl5fdd37ce/mac)
 - [Ubuntu](https://help.ubuntu.com/stable/ubuntu-help/display-dual-monitors.html) 

## Starting It Up 

### BIOS

 - **Drivers** (AKA *services*) contain instructions the CPU needs to understand external devices.

 - The CPU doesn't know there are devices it can talk to, so it connects to something called the BIOS.

 - The **Basic Input/Output Services (BIOS)** helps initialize the hardware in the computer, and gets the operating system up and running.
   - The BIOS is not stored on the hard drive;
     - Instead, the BIOS is stored on the motherboard, in a special **read-only memory chip (ROM chip)**
     - ROM is not volatile like RAM, and doesn't clear when the computer is turned off
  - When the operating system loads, the BIOS loads drivers from non-essential devices directly from the hard drive.

 - The **UEFI (Unified Extensible Firmware Interface)** performs the same function as BIOS; but is a modernized and superior format. 
  - Most modern computers come with UEFI, and will become the BIOS standard.

 - Computers run a **power-on self test (POST)** to figure out which hardware is on the computer, happening before the BIOS initializes anything.
   - Since the screen is not active, the computer usually communicates via a beep.

- The **CMOS battery** stores basic data about booting the computer (like date, time, and how to start up)
  - You can alter these in the CMOS or BIOS settings menu.

- **Reimaging** involves wiping and reinstalling an operating system, and is a common IT task. This process involves navigating the computer's BIOS.

### Putting It All Together

 - **Electrostatic discharge** (AKA, *static electricity*) is a major hazard to computer components.
   - You should always ground yourself before working on physical components of a computer.

 - Keep computer components in anti-static bags until you need to access them for your computer.

 - **Standoffs** are used to raise and attach your motherboard to the case.

 - CPUs have a marker that has to align with the CPU socket on the motherboard.
   - Again: Make sure your CPU is compatible with your motherboard.

 - Before you attach the heat sink, apply thermal paste to the CPU.

 - Align your RAM/DIMM sticks as good practice (it protects your pins from damage)
   - (Read your motherboard's manual to learn about its RAM slots.)

 - Create a wind tunnel that takes in air, blows it over the components, then pushes it all out back.

 - Keep cables off to the side, so as not to damage the motherboard.

### Mobile Device Repair

 - Always refer to the **return merchandise authorization (RMAO** policy before you do anything.

 - **Factory reset** Removes all data, apps, and customizations from the device.

 - When working on mobile devices, follow the same safeguards as you would with a computer:
   - Protect against static discharge;
   - Use the proper tools;
   - Keep parts organized and labeled;
   - Take pictures along the way;
   - Follow vendor documentation;
   - Test the device to ensure it works.


--- 

## Questions for review

### Keywords

<details>
  <summary>What are ports?</summary>
  <p>Ports are connection points that we can connect devices to that extend the functionality of our computer.</p>
</details>

<details>
  <summary>What is a CPU?</summary>
  <p>The central processing unit (CPU) is the brain of the computer, it does all the calculations and data processing</p>
</details>

<details>
  <summary>What is RAM?</summary>
  <p>Random access memory (RAM) is the computer's short term memory.</p>
</details>

<details>
  <summary>What is a hard drive?</summary>
  <p>The hard drive holds all of the data.</p>
</details>

<details>
  <summary>What is a motherboard?</summary>
  <p>The motherboard is the body or circulatory system of the computer, that connects all the pieces together.</p>
</details>

<details>
  <summary>What is a power supply?</summary>
  <p>The power supply converts electricity from the wall outlet into a format the computer can use.</p>
</details>

~

<details>
  <summary>What is a program?</summary>
  <p>Programs are instructions that tell the computer what to do.</p>
</details>

<details>
  <summary>What is a data bus?</summary>
  <p>A data bus is a network of wires connecting computer components, which send voltage to wires to represent on (1) or off (0).
</p>
</details>

<details>
  <summary>What is an internal data bus?</summary>
  <p>The internal data bus communicates between internal components like video cards and memory.</p>
</details>

<details>
  <summary>What is the external data bus?</summary>
  <p>The external data bus (EDB) connects the computer to peripherals, such as a USB or SCSI device.</p>
</details>

<details>
  <summary>What is a register?</summary>
  <p>Registers store the data the CPU works with.</p>
</details>

<details>
  <summary>What is a memory controller chip?</summary>
  <p>The memory controller chip (MCC) is a bridge between the CPU and the RAM, like a brain's nerve controlling thought or memory.</p>
</details>

<details>
  <summary>What is an address bus?</summary>
  <p>The address bus connects the CPU to the MCC; it sends the location of data, so the MCC can lo</p>
</details>

<details>
  <summary>What is cache?</summary>
  <p>Cache i smaller than RAM, but stores more frequently-used data in an easier and faster-to-use way.</p>
</details>

<details>
  <summary>What is a clock wire?</summary>
  <p>A clock wire lets the CPU know it can start performing calculations, triggered by a clock cycle.</p>
</details>

<details>
  <summary>What is a clock cycle?</summary>
  <p>A clock cycle is when voltage is sent to the clock wire, and refers to the entire process of a clock wire-CPU interaction.</p>
</details>

<details>
  <summary>What is overclocking?</summary>
  <p>Overclocking is a way to increase a CPU's clock cycle rate, to improve performance.</p>
</details>

~

<details>
  <summary>What is an instruction set?</summary>
  <p>An instruction set is a list of instructions the CPU can run (hard-coded and varying by manufacturer).</p>
</details>

<details>
  <summary>What is a heat sink?</summary>
  <p>A heat sink pulls heat from the CPU and dissipates it with a fan or other medium.</p>
</details>

<details>
  <summary>What is a peripheral?</summary>
  <p>Peripherals are external devices that can connect to a computer.</p>
</details>

<details>
  <summary>What is an expansion slot?</summary>
  <p>Expansion slots allow for increased computer functionality.</p>
</details>

<details>
  <summary>What is ATA?</summary>
  <p>Advanced technology attachment (ATA) is a standard physical interface for connecting storage devices within a computer.</p>
</details>

<details>
  <summary>What is NVM Express?</summary>
  <p></p>
</details>

<details>
  <summary>What is amperage?</summary>
  <p>Measured in amps, amperage is the pulling of electricity as <em>as needed</em>; whereas voltage pushes all electricity.</p>
</details>

<details>
  <summary>What is wattage?</summary>
  <p>Wattage is the amount of volts and amps required by a device.</p>
</details>

<details>
  <summary>What is a driver?</summary>
  <p>Drivers contain instructions the CPU needs to understand external devices.</p>
</details>

<details>
  <summary>What is the BIOS?</summary>
  <p>The basic input/output services (BIOS) helps initialize the hardware in the computer, and gets the operating system up and running.</p>
</details>

<details>
  <summary>What is the UEFI?</summary>
  <p>The unified extensible firmware interface (UEFI) functions like the BIOS, but is a modernized, superior format.</p>
</details>

<details>
  <summary>What is the POST?</summary>
  <p>The power-on self test (POST) figures out which hardware is on the computer, and happens before the BIOS initializes anything.</p>
</details>

<details>
  <summary> What is the CMOS?</summary>
  <p>The CMOS is a battery, which stores basic data about booting the computer.</p>
</details>

~

<details>
  <summary>What is a factory reset?</summary>
  <p>A factory reset removes all data, apps, and customization from a device.</p>
</details>

~


### Concepts
<details>
  <summary>What are the two aspects of a chipset?</summary>
  <p>The Northbridge connects RAM and video cards; and the Southbridge maintains I/O controllers (like hard drives and USB devices).</p>
</details>

<details>
  <summary>What is the standard expansion bus today?</summary>
  <p>Peripheral Component Interconnect (PCI) Express</p>
</details>

<details>
  <summary>What are the two most common motherboard form factors?</summary>
  <p>Advanced Technology eXtended (ATX) and Information Technology eXtended</p>
</details>

<details>
  <summary>What are the differences between HDD and SSD?</summary>
  <p>HDD have more moving parts, are more fragile, and less expensive; SSD are far more stabile, but more expensive.</p>
</details>

<details>
  <summary>What is the most common ATA drive today?</summary>
  <p>The Serial ATA (SATA) drive</p>
</details>

<details>
  <summary>What does "hot-swappable" mean?</summary>
  <p>"Hot-swappable" refers to a peripheral or component that can be removed or added while the computer is running.</p>
</details>

<details>
  <summary>What are the most common USB connection types today?</summary>
  <p>USB 2.0; USB 3.0; USB 3.1</p>
</details>

<details>
  <summary>What is the difference between Mb and MB?</summary>
  <p>A MB is a *megabyte*, a unit of data storage; a Mb is a *megabit*, a unit of data transfer rate.</p>
</details>

<details>
  <summary>Why should you always ground yourself before working on physical components of a computer?</summary>
  <p>Static electricity is a major hazard to computer components.</p>
</details>

<details>
  <summary>How do you assemble a (desktop) computer?</summary>
  <p></p>
</details>
