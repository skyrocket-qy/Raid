# Go RAID Simulator

A command-line tool for simulating and demonstrating the functionality of various RAID (Redundant Array of Independent Disks) levels. This project provides a hands-on way to understand how different RAID configurations handle data storage and fault tolerance.

## What is RAID?

RAID is a data storage virtualization technology that combines multiple physical disk drive components into one or more logical units for the purposes of data redundancy, performance improvement, or both.

This simulator implements the following RAID levels:

*   **RAID 0 (Striping):** Data is split evenly across two or more disks. It offers improved performance but no redundancy. The failure of one disk results in the loss of all data.
*   **RAID 1 (Mirroring):** Data is duplicated across two or more disks. It provides excellent redundancy at the cost of storage capacity.
*   **RAID 5 (Striping with Parity):** Data is striped across multiple disks, with parity information distributed among them. It can withstand the failure of a single disk without data loss.
*   **RAID 6 (Striping with Double Parity):** Similar to RAID 5, but with an additional parity block. It can tolerate the failure of up to two disks.
*   **RAID 10 (Mirroring and Striping):** A hybrid RAID combining the mirroring of RAID 1 with the striping of RAID 0. It offers both high performance and high redundancy.

## Usage

To run the simulation, you need to have Go installed.

1.  Clone the repository.
2.  Navigate to the project directory.
3.  Run the simulation with the desired RAID level as a command-line argument:

```bash
go run . <raid_number>
```

Where `<raid_number>` can be one of the following: `0`, `1`, `5`, `6`, `10`.

### Example

To simulate RAID 5:

```bash
go run . 5
```

## Simulation Explained

The simulation performs the following steps:

1.  **Initialization:** It creates a set of virtual disks in memory.
2.  **Writing Data:** It writes the string "Hello World!" to the RAID array.
3.  **Simulating Disk Failure:** It clears the data from one of the disks to simulate a failure.
4.  **Data Recovery:** It attempts to read the original string back from the (now degraded) RAID array.

The output will show the data before and after the disk failure, demonstrating the fault tolerance of the chosen RAID level. For RAID 0, the read after failure is expected to fail, while for other levels, it should succeed.

## Code Structure

The project is structured as follows:

*   `main.go`: The main application entry point, handling command-line arguments and running the simulation.
*   `domain.go`: Defines the core `Raid` interface that all RAID implementations adhere to.
*   `disk.go`: Implements the in-memory virtual disk used by the simulations.
*   `raid0.go`, `raid1.go`, `raid5.go`, `raid6.go`, `raid10.go`: Individual implementations for each of the supported RAID levels.
*   `go.mod`, `go.sum`: Go module files for dependency management.

This structure makes it easy to extend the project with new RAID implementations.
