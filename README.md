**NextGen In A Box (NGIAB)**

**Run the NextGen National Water Resources Modeling Framework locally with ease.**

NGIAB provides a containerized and user-friendly solution for running the NextGen framework, allowing you to control inputs, configurations, and execution on your local machine.

| | |
| --- | --- |
| ![alt text](https://ciroh.ua.edu/wp-content/uploads/2022/08/CIROHLogo_200x200.png) | Funding for this project was provided by the National Oceanic & Atmospheric Administration (NOAA), awarded to the Cooperative Institute for Research to Operations in Hydrology (CIROH) through the NOAA Cooperative Agreement with The University of Alabama (NA22NWS4320003). |

[![ARM Build and push final image](https://github.com/CIROH-UA/NGIAB-CloudInfra/actions/workflows/docker_image_main_branch.yml/badge.svg)](https://github.com/CIROH-UA/NGIAB-CloudInfra/actions/workflows/docker_image_main_branch.yml)
[![X86 Build and push final image](https://github.com/CIROH-UA/NGIAB-CloudInfra/actions/workflows/docker_image_main_x86.yml/badge.svg)](https://github.com/CIROH-UA/NGIAB-CloudInfra/actions/workflows/docker_image_main_x86.yml)

**Why NextGen In A Box?**

- **Run NextGen Locally:** Experiment with the framework and customize configurations on your local machine.
- **Control Over Inputs:** Choose specific regions or basins for analysis and modify input data as needed.
- **Simplified Setup:** Utilize Docker containers for effortless deployment, avoiding complex software installations.
- **Open Research Practices:** Promote transparency and reproducibility through open-source tools like Git and GitHub.

**Case Study:** This repository demonstrates running NWM for Provo River Basin, UT 

**Repository Contents:**

- Dockerfile for running the NextGen Framework
- Guide script (guide.sh) for easy execution
- README with instructions and documentation

**Getting Started**

**Prerequisites**

**Windows:**
1. **Install WSL:** Head over to Microsoft's official documentation and follow their comprehensive guide on installing WSL: https://learn.microsoft.com/en-us/windows/wsl/install
2. **Install Docker Desktop:** Begin by downloading and installing Docker Desktop from the official website: https://docs.docker.com/desktop/install/windows-install/#install-docker-desktop-on-windows
3. **Start Docker Desktop:** After installation, launch the Docker Desktop application.
4. **Open WSL as Admin:** Right-click on the WSL icon and select "Run as Administrator".
5. **Verify Installation:** In the WSL window, type the command docker ps -a to check if Docker is running correctly. This command should display a list of Docker containers.

**Mac:**
1. **Install Docker Desktop:** Download and install Docker Desktop for Mac from: https://docs.docker.com/desktop/install/mac-install/
2. **Start Docker Desktop:** Launch the Docker Desktop application once the installation is complete.
3. **Open Terminal:** Open the Terminal application on your Mac.
4. **Verify Installation:** Similar to Windows, use the command docker ps -a in the Terminal to verify Docker is functioning as expected.

**Linux:**
1. **Install Docker:** The installation process for Linux varies depending on your distribution. Refer to the official documentation for detailed instructions: https://docs.docker.com/desktop/install/linux-install/
2. **Start Docker and Verify:** Follow the same steps as described for Mac to start Docker and verify its installation using the docker ps -a command in the terminal.

- **Input Data:**
  - **Download Sample Data:** Use the provided commands to download sample data for the Sipsey Fork case study.
  - **To generate your own data:** Refer to the [NGIAB-datapreprocessor](https://github.com/AlabamaWaterInstitute/NGIAB_data_preprocess) for instructions on generating custom input data.
  - **To generate your own data and run using NGIAB:** Refer to the [ngen-datastream repository](https://github.com/CIROH-UA/ngen-datastream/tree/main) for instructions on generating custom input data.

This section guides you through downloading and preparing the sample input data for the NextGen In A Box project.

**Step 1: Create Project Directory**

- **Linux/Mac:** Open your terminal and go to your desired folder where you want to checkout repo and ngen-data folder and run the following commands:
```bash
mkdir -p NextGen/ngen-data
```

```bash
cd NextGen/ngen-data
```
- **WSL (Right click and run as Admin):** Open WSL with administrator privileges and execute:
```bash
cd /mnt/c/Users/<Folder>
```

```bash
mkdir -p NextGen/ngen-data
```

```bash
cd NextGen/ngen-data
```
**Step 2: Download Sample Data**

- **Linux/Mac/Windows WSL:** Use wget to download the compressed data file:
```bash
wget --no-parent https://ciroh-ua-ngen-data.s3.us-east-2.amazonaws.com/AWI-006/AWI_16_2853886_006.tar.gz
```

**Step 3: Extract and Rename**

- **All Platforms:** Extract the downloaded file and optionally rename the folder:
```bash
tar -xf AWI_16_2853886_006.tar.gz
```
### Below is Optional: Rename the folder
```bash
mv AWI_16_2853886_006 my_data
```
Now you have successfully downloaded and prepared the sample input data in the NextGen/ngen-data directory. Remember to replace "my_data" with your preferred folder name if you choose to rename it.

### Case Study Map for the Provo River Basin, UT 

![Provo River Basin](https://github.com/arpita0911patel/NGIAB-CloudInfra/assets/28275758/dfe3bfab-9b1f-4271-880e-abf4d8db715f)

**Running NGIAB**

1. **Clone the Repository:**
Go to the folder created earlier during step #1 above

```bash
cd NextGen
git clone https://github.com/CIROH-UA/NGIAB-CloudInfra.git
```
```bash
cd NGIAB-CloudInfra
```

2. **Run the Guide Script:**
```bash
./guide.sh
```

3. **Follow the prompts:**
    - **Input Data Path:** Enter the path to your downloaded or generated input data directory. (e.g NextGen/ngen-data/my_data)
    - **Run Mode:** Choose between parallel or serial execution based on your preferences.
      The script pulls the related image from the awiciroh DockerHub, based on the local machine's architecture:
      ```
      For Mac with apple silicon (arm architecture), it pulls awiciroh/ciroh-ngen-image:latest.
      For x86 machines, it pulls awiciroh/ciroh-ngen-image:latest-x86.
      ```
      Example NGEN run command for parallel mode: 
      ```bash
      mpirun -n 10 /dmod/bin/ngen-parallel ./config/wb-2853886_subset.gpkg all ./config/wb-2853886_subset.gpkg all ./config/realization.json /ngen/ngen/data/partitions_10.json
      ```
      
      Example NGEN run command for serial mode: 
      ```bash
      /dmod/bin/ngen-serial ./config/wb-2853886_subset.gpkg all ./config/wb-2853886_subset.gpkg all ./config/realization.json
      ```
    - **Select Files (automatically):** Script selects specific catchment, nexus, and realization files based on input data.
    - After the model has finished running, the script prompts the user whether they want to continue.
    - If the user selects 1, the script opens an interactive shell.
    - If the user selects 2, then the script exits.

**Output:**
- Model outputs will be saved in the outputs folder within your input data directory. (e.g '.../NextGen/ngen-data/my_data/')
- Refer to the provided example for post-processing and visualizing streamflow data.
  
**Additional Resources:**

- [Next Generation Water Modeling Engine and Framework Prototype](https://github.com/NOAA-OWP/ngen)
- [NGIAB_data_preprocessor](https://github.com/AlabamaWaterInstitute/NGIAB_data_preprocess)
- [ngen-datastream Repository](https://github.com/CIROH-UA/ngen-datastream/tree/main)
