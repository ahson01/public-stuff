---
title: "Download Websites"
date: "2025-03-18"
tags: ["wget", "web", "bash"]
---

# 🌐 Downloading Files from a Website with `wget`

Learn how to download files from a website using the versatile `wget` tool! This guide covers downloading an entire website, limiting download depth, and focusing on specific file types.

## Step 1: Install `wget` 📦

1. **Check if `wget` is Installed**:
   Most Linux and macOS systems come with `wget` pre-installed. Open your terminal and check if you have it:

   ```bash
   wget --version
   ```

   If you see version information, you're good to go! 🎉

2. **Install `wget` (if necessary)**:
   If you don't have `wget`, install it using the appropriate command for your operating system:

   - **Ubuntu/Debian**:
     ```bash
     sudo apt-get install wget
     ```

   - **macOS**:
     ```bash
     brew install wget
     ```

   - **Windows**:
     Download the installer from [GNU's official website](https://eternallybored.org/misc/wget/) or use a package manager like [Chocolatey](https://chocolatey.org/):
     ```bash
     choco install wget
     ```

## Step 2: Download the Website 🚀

1. **Download the Entire Website**:
   To download an entire website recursively, use the following command:

   ```bash
   wget --recursive --no-clobber --page-requisites --html-extension --convert-links --restrict-file-names=windows --no-parent https://example.com/
   ```

2. **Command Explanation**:
   - `--recursive`: Download the entire website recursively.
   - `--no-clobber`: Avoid overwriting existing files.
   - `--page-requisites`: Download all files required to properly display the pages (e.g., CSS, JS, images).
   - `--html-extension`: Save HTML files with a `.html` extension.
   - `--convert-links`: Modify links for offline viewing.
   - `--restrict-file-names=windows`: Make filenames compatible with Windows.
   - `--no-parent`: Prevent downloading files from parent directories.

## Step 3: Download Specific File Types 🎯

1. **Download Only Non-HTML Files**:
   To download only specific file types (like PDF, DOC, or media files) and exclude HTML, CSS, and JavaScript files, use:

   ```bash
   wget --recursive --no-clobber --convert-links --restrict-file-names=windows --no-parent --accept pdf,doc,docx,xls,xlsx,ppt,pptx,zip,rar,tar.gz,mp3,mp4,avi --reject html,css,js https://example.com/
   ```

2. **Explanation of the Options**:
   - `--accept pdf,doc,docx,...`: Downloads only the specified file types (e.g., PDFs, documents, archives, media).
   - `--reject html,css,js`: Excludes HTML, CSS, and JavaScript files from the download.

## Step 4: Optional Settings ⚙️

1. **Ignore `robots.txt`**:
   Some sites prevent automatic downloads using a `robots.txt` file. To bypass these restrictions, use:

   ```bash
   wget --execute robots=off --recursive --no-clobber --convert-links --restrict-file-names=windows --no-parent https://example.com/
   ```

2. **Add a Delay Between Requests**:
   To avoid overloading the server, introduce a delay with the `--wait` option:

   ```bash
   wget --wait=1 --recursive --no-clobber --convert-links --restrict-file-names=windows --no-parent https://example.com/
   ```

   This command waits 1 second between requests.

3. **Limit the Download Depth**:
   Control how many levels deep you want to download by using the `-l` option:

   ```bash
   wget -r -l 3 --no-clobber --convert-links --restrict-file-names=windows --no-parent https://example.com/
   ```

   This limits the download to 3 levels deep.

## Step 5: Verify the Download 🕵️‍♂️

1. **Check the Directory**:
   After the download is complete, navigate to the directory where you ran the `wget` command. You should see the website's files and folders organized as they were on the server.

2. **Open the Files Offline**:
   Open the downloaded files in your preferred application to view them offline. If you focused on specific file types, only those files should be present! 📂

---
