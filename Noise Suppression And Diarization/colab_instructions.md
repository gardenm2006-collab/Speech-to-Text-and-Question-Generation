# 🚀 Step-by-Step Guide: Running the Pipeline in Google Colab

Follow these steps to run the consolidated noise suppression and speaker diarization pipeline successfully in Google Colab:

---

## 🛠️ Step 1: Set Up GPU Runtime
1. Open the [noise_suppression_and_diarization.ipynb](file:///Users/mybook/Downloads/SOPHOMORE/GIT/Speech-to-Text-and-Question-Generation/noise_suppression_and_diarization.ipynb) notebook in Google Colab.
2. In the top menu, click **Runtime** -> **Change runtime type**.
3. Under **Hardware accelerator**, select **T4 GPU**.
4. Click **Save**.

---

## 🔑 Step 2: Set Up Hugging Face Secrets Access
1. Visit **[pyannote/speaker-diarization-community-1](https://huggingface.co/pyannote/speaker-diarization-community-1)** and accept the user conditions.
2. Go to your **Hugging Face Account Settings** -> **Access Tokens** and create a token with **Read** access.
3. In your Colab left-side navigation bar, click the **Secrets Manager (key icon 🔑)**.
4. Add a new secret:
   * **Name**: `HF_TOKEN`
   * **Value**: *Paste your Hugging Face read access token*
5. Toggle the **Notebook access** switch to **ON** for this secret.

---

## 📦 Step 3: Install Core Dependencies (Step 0 in Notebook)
1. Run the **Step 0: Setup & Core Dependencies** code cell.
2. > [!IMPORTANT]
   > If Colab displays a popup or warning saying *"Your session crashed for an unknown reason"* or asks you to **"RESTART RUNTIME"** / **"RESTART SESSION"**, click it. This is normal and applies the package updates cleanly.

---

## 🔑 Step 4: Run Initialization (Step 1 in Notebook)
1. Run the **Step 1: Configuration & Hugging Face Access** cell.
2. Verify that it outputs:
   * `[SUCCESS] Retrieved Hugging Face access token (HF_TOKEN) from Secrets.`
   * `[INFO] Using device: cuda` (confirms GPU is successfully active).

---

## 📁 Step 5: Mount Google Drive & Set Paths (Step 2 in Notebook)
1. In the **Step 2: Interactive Parameter Configurations** form, customize:
   * `input_audio_path`: The path of your raw audio file in Drive (e.g. `/content/drive/MyDrive/MyFolder/audio.m4a`).
   * `cleaned_audio_folder`: Subfolder where the denoised WAV file will be saved.
   * `diarization_output_folder`: Folder where diarization reports and text logs will be exported.
2. Run the cell.
3. Colab will display a prompt: *"Permit this notebook to access your Google Drive files?"*
4. Click **Connect to Google Drive** and authorize your account.

---

## 🏃‍♂️ Step 6: Execute the Audio & Diarization Pipeline (Steps 3 to 6)
Run the remaining cells sequentially:
1. **Step 3 (Noise Suppression)**: Standardizes audio in memory to 16kHz mono and reduces background static. The clean file is saved to your Drive.
2. **Step 4 (Pyannote Diarization)**: Runs speaker diarization community models on the clean audio.
3. **Step 5 (Timeline Refinement)**: Groups adjacent speech blocks and calculates speaking statistics.
4. **Step 6 (Multi-Format Serialization)**: Exports all files, including:
   * `{audio_name}_diarization_timestamps.txt` (requested timestamp log).
   * `{audio_name}_diarization_report.md` (premium markdown participation report).
   * CSV, JSON, and RTTM files.
