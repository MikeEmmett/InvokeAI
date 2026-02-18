# InvokeAI on Google Colab

This project provides a Google Colab notebook for running [InvokeAI](https://invoke-ai.github.io/InvokeAI/), an AI image generation tool. The notebook automates the setup process, allows importing custom models, and can save generated images to Google Drive.

**Note:** This notebook has been tested and is confirmed working with InvokeAI version 5.15.0. It is designed for InvokeAI version 5.7.0 and later. It does not support versions older than 5.5.0.

## Table of Contents

- [Getting Started](#getting-started)
  - [Directly from GitHub (Recommended)](#directly-from-github-recommended)
  - [Manually Upload to Google Drive](#manually-upload-to-google-drive)
  - [Manual Setup in Google Colab](#manual-setup-in-google-colab)
- [Notebook Link](#notebook-link)
- [How to Use](#how-to-use)
- [Configuration Options](#configuration-options)
  - [Instance Type](#instance-type)
  - [Connection Type](#connection-type)
  - [Instance Selector](#instance-selector)
  - [InvokeAI Version](#invokeai-version)
  - [Model Management](#model-management)
  - [Memory Management](#memory-management)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)
- [Support](#support)

---

## Getting Started

You have a few options to get started with the InvokeAI Colab notebook:

#### Directly from GitHub (Recommended)
1. Open [Google Colab](https://colab.research.google.com).
2. A dialog box should appear. If not, go to "File" > "Open Notebook" (Ctrl + O).
3. Select the "GitHub" tab.
4. In the search box, type `MikeEmmett/InvokeAI`.
5. Select the notebook file: `InvokeAI_in_Google_Colab.ipynb`.

#### Manually Upload to Google Drive
1. Download the notebook: Click "Code" at the top of this repository page, then choose "Download ZIP".
2. Extract the downloaded ZIP file.
3. Upload `InvokeAI_in_Google_Colab.ipynb` to your Google Drive.
4. Open the notebook from your Google Drive or through [Google Colab](https://colab.research.google.com) by selecting the "Google Drive" tab in the "Open Notebook" dialog.
   *Note: Using Google Drive desktop or mobile apps to launch the notebook will not work.*

#### Manual Setup in Google Colab
1. Create a new Google Colab project: [https://colab.research.google.com/#create=true](https://colab.research.google.com/#create=true).
2. Enable GPU acceleration: Go to "Edit" > "Notebook Settings" > "Hardware accelerator" and select "GPU" (e.g., T4 GPU).
3. Open the `InvokeAI_in_Google_Colab.ipynb` file from this repository.
4. Copy and paste each code cell from the downloaded notebook into your new Colab project, from top to bottom.

---

## Notebook Link

You can directly open the notebook in Google Colab using this link:

[Open InvokeAI in Google Colab](https://colab.research.google.com/github/MikeEmmett/InvokeAI/blob/main/Invokeai_in_google_colab.ipynb)

---

## How to Use

1.  **Open the notebook** using one of the methods described in [Getting Started](#getting-started).
2.  **Configure the settings** in the first code cell ("1. Configuration") according to your preferences. Details about each option can be found in the [Configuration Options](#configuration-options) section below.
3.  **Run the cells sequentially:**
    *   Click "Runtime" > "Run All" to execute all cells in order.
    *   Alternatively, click the "play" button next to each cell, starting from the top. You don't need to wait for a cell to finish before running the next one; they will be added to an execution queue.
4.  **Cell 1: Configuration:** Set your desired options for storage, connection, InvokeAI version, etc.
5.  **Cell 2: Installation:** This cell installs InvokeAI and its dependencies. It takes approximately 4-5 minutes.
6.  **Cell 3: Start InvokeAI:** This cell launches the InvokeAI web interface.
    *   It takes about 15 seconds to generate the access URL and another 30 seconds for the application to be fully operational.
    *   Follow the instructions printed in the output of this cell to access the InvokeAI web UI. This usually involves copying an IP address and pasting it into a form on the page opened by the generated URL.
7.  **Access InvokeAI:** Once the setup is complete and the web server is running, a URL will be provided. Open this URL in your browser to start using InvokeAI.
8.  **Stopping the instance:** If you are using "Google_Drive" mode, it is **strongly recommended** to stop the execution of the "Start InvokeAI" cell when you are finished. This ensures a graceful shutdown and prevents potential data corruption if information is still being uploaded to your Drive. Do this by clicking the "stop" button on that cell. Simply closing the tab or using "Disconnect and Delete this runtime" might lead to issues.

---

## Configuration Options

The first cell in the notebook ("1. Configuration") allows you to customize various aspects of your InvokeAI instance.

### Instance Type
Determines where your models, images, and database are stored.
*   `Google_Drive`: Stores everything in your Google Drive. The space required depends on the number and type of models used.
*   `Temporary`: Everything is stored in the Colab runtime environment. All data will be lost when the runtime ends or crashes. **Make sure to download your images if you use this option.**

### Connection Type
How you will connect to the InvokeAI web interface.
*   `NGROK` (Recommended): Highly stable but requires an NGROK authtoken.
    *   Sign up for a free token at [https://dashboard.ngrok.com/get-started/your-authtoken](https://dashboard.ngrok.com/get-started/your-authtoken).
    *   Enter the token in the `ngrok_token` field.
*   `NGROK_APT`: An alternative NGROK setup that runs as a Linux service. Also requires an `ngrok_token`.
*   `Localtunnel`: Slower and sometimes less reliable than NGROK, but requires no setup or token.
*   `Cloudflare`: Uses Cloudflare Quick Tunnels. Usually stable, requires no setup or token.

### Instance Selector
Allows you to have multiple, separate InvokeAI instances.
*   `Default`: Files are stored in `/content/invokeai` (for Temporary type) or `/content/drive/MyDrive/InvokeAI` (for Google_Drive type).
*   `Custom Name` (e.g., "Anime", "Photorealism"): Files are stored in a subfolder within the default location (e.g., `/content/drive/MyDrive/InvokeAI/CustomInstances/Anime`).

### InvokeAI Version
Specify the version of InvokeAI to install.
*   `Default`: Installs the latest stable release of InvokeAI.
*   `Specific Version` (e.g., "5.7.2", "5.6.1"): Installs the specified version. Versions 5.7.2+ are recommended for full feature compatibility. Versions before 5.0.0 will likely not work.

### Model Management
*   Model management is done within the InvokeAI application via the "Model Manager" on the left-hand side.
*   `GDrive_Import` (Checkbox): If using "Temporary" Instance Type, you can tick this box to mount your Google Drive solely for importing models. The path `/content/drive/MyDrive/` will be available in the Model Manager.

### Memory Management
InvokeAI offers two methods for managing models in VRAM.
*   `CUDA` (Recommended for InvokeAI 5.7.2+): Typically outperforms `pytorch`, reducing peak VRAM usage and potentially improving generation speeds. Not suitable for CPU mode.
    *   If CUDA is selected but no GPU is available at runtime, the notebook now automatically falls back to `pytorch` to avoid startup failures.
*   `pytorch`: The alternative memory allocator. Use this for older InvokeAI versions or if you intend to run in CPU mode (not generally recommended on Colab).

---

## FAQ

This section is based on the FAQ within the Colab notebook.

*   **Images are taking a LONG time to generate (e.g., ~30 mins for a 512x512 image).**
    *   You might be running in CPU mode. Click the "RAM / Disk" button in the top right of Colab. If "GPU RAM" isn't listed, you're not on a GPU instance.
    *   Ensure a GPU is selected in "Edit" > "Notebook settings" (e.g., "T4 GPU").

*   **It is taking a while to even start loading.**
    *   If it's a new instance or you're changing models, the model needs to be loaded. If using "Google Drive," the model is downloaded to the runtime first, which can take time, especially for large models (XL: 5-10 mins, FLUX: 20+ mins).

*   **No link is given to me for Localtunnel/NGROK/Cloudflare?**
    *   Check the status of the services:
        *   Localtunnel: [https://downforeveryoneorjustme.com/localtunnel.me](https://downforeveryoneorjustme.com/localtunnel.me)
        *   NGROK: [https://status.ngrok.com](https://status.ngrok.com)
        *   Cloudflare: [https://www.cloudflarestatus.com/](https://www.cloudflarestatus.com/)

*   **I get an error "You have recently exceeded an allowance, most recently at (Time)".**
    *   This usually means you've hit a Google Colab usage limit, often from frequent starting/stopping of instances. It might not affect functionality. If it does, you may need to wait (e.g., 1 hour) for soft allowances to reset.

*   **How much longer can my instance run for today?**
    *   Click the "RAM / DISK" button in the top right of Colab. It will show an estimate like "At your current usage level, this runtime may last up to X hours Y minutes".

*   **My instance disconnects while I'm using it.**
    *   Using web interfaces this way can be against Google Colab's Terms of Service. If you don't interact with the Colab tab for 15+ minutes, it might hibernate. Switch back to the Colab tab periodically to keep it active.

*   **Are there any known issues?**
    *   Major known issues are typically updated in the header at the top of the notebook, above the "Introduction."

*   **I want to make my own changes to this file and save them.**
    *   In Colab, go to "File" > "Save a copy in Drive."

*   **Is this maintained frequently?**
    *   This project is maintained by a solo developer. Issues can be raised on GitHub: [https://github.com/MikeEmmett/InvokeAI/issues](https://github.com/MikeEmmett/InvokeAI/issues).

*   **I am using Google Drive and I want to reset everything.**
    *   Go to [https://drive.google.com/drive/my-drive](https://drive.google.com/drive/my-drive).
    *   To completely reset (delete all data), delete the "InvokeAI" folder.
    *   To archive your models/images before resetting, rename the "InvokeAI" folder.

*   **I don't understand the configuration options...**
    *   Experiment! The notebook is designed to work with default settings ("Runtime" > "Run all"). It will connect to your Google Drive and use Localtunnel. Follow the on-screen instructions in the final step.

---

## Contributing

Contributions are welcome! If you have improvements, bug fixes, or new features you'd like to add:

1.  **Fork the repository.**
2.  **Create a new branch** for your changes (e.g., `git checkout -b feature/my-new-feature` or `git checkout -b fix/issue-number`).
3.  **Make your changes** in the `Invokeai_in_google_colab.ipynb` notebook.
4.  **Test your changes thoroughly** to ensure they work as expected and don't break existing functionality.
5.  **Commit your changes** with clear and descriptive commit messages.
6.  **Push your branch** to your forked repository.
7.  **Open a Pull Request** to the `main` branch of this repository. Please provide a detailed description of your changes in the PR.

If you find any issues or have suggestions, please open an issue on the [GitHub Issues page](https://github.com/MikeEmmett/InvokeAI/issues).

---

## License

This project is open-source and available under the [Apache License 2.0](LICENSE). InvokeAI, which this notebook helps you run, also uses the Apache License 2.0. You can find more details about the InvokeAI license in their [documentation](https://invoke-ai.github.io/InvokeAI/getting-started/LICENSE/).

---

## Support

If you find this project helpful, consider supporting the developer:

ETH: `0x94390B2b3890c768De13e04BaE883F7b222690C2`
