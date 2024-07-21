
---

## How to Build a Custom ROM Using Pre-Built Trees

### Prerequisites
1. **Powerful PC Configuration:** Ensure you have a powerful PC with at least:
   - 8-core CPU
   - 32 GB RAM
   - 32 GB ZRAM
   - 400 GB SSD
   This configuration should allow you to complete the build within approximately 5 hours.

### Steps to Build a Custom ROM

#### 1. Create a GitHub Account
If you don't already have a GitHub account, create one at [GitHub](https://github.com).

#### 2. Clone or Download ROM Source
1. **Create a ROM folder:**
   ```bash
   mkdir rom
   cd rom
   ```

2. **Initialize the repository:**
   Find your favorite ROM's GitHub manifest. For example, to build Project Blaze, use:
   ```bash
   repo init -u https://github.com/ProjectBlaze/manifest -b 14-QPR3 --depth 1
   ```
   Using `--depth 1`, saves GBs of space by only downloading the latest commits.

3. **Sync the repository:**
   ```bash
   repo sync -c -j$(nproc --all) --force-sync --no-clone-bundle --no-tags --optimized-fetch --prune
   ```
   You can adjust `-j` to match the number of CPU cores you have (e.g., `-j8` for 8 cores).

4. **Set up Git username and email:**
   ```bash
   git config --global user.email "YOUR_EMAIL"
   git config --global user.name "YOUR_USERNAME"
   ```

#### 3. Obtain Device Source
You will need the device tree, vendor tree, and kernel tree. In some cases, you might also need common trees.

1. **Find these trees on GitHub:**
   Search for `device xiaomi [device_name]`, `vendor xiaomi [device_name]`, and `kernel xiaomi [device_name]`. Ensure all trees are from the same developer to avoid compatibility issues.

2. **Clone the repositories:**
   ```bash
   cd rom
   git clone [device_repo_url] device/xiaomi/violet
   git clone [vendor_repo_url] vendor/xiaomi/violet
   git clone [kernel_repo_url] kernel/xiaomi/violet
   ```
   The kernel directory structure might vary, so check `BoardConfig.mk` in your device tree.

#### 4. Bring Up Your Device Tree
This step varies depending on the ROM you are building. For example, in Project Blaze:
1. **Edit files:**
   - `lineage_violet.mk` or `aosp_violet.mk` to `blaze_violet.mk`
   - `androidproducts.mk`: Change `lineage` or `aosp_violet` to `blaze_violet`
   - Edit the ROM config file within `blaze_violet.mk`:
     ```mk
     $(call inherit-product, vendor/blaze/config/common_full_phone.mk)
     ```

2. **Save changes:**
   - Press `Ctrl+O`, then `Ctrl+X`

#### 5. Build the ROM
1. **Set up the environment:**
   ```bash
   . build/envsetup.sh
   ```

2. **Lunch the build target:**
   ```bash
   lunch blaze_violet-user
   ```

3. **Start the build:**
   ```bash
   make bacon
   ```
   or
   ```bash
   mka bacon
   ```

Within a few hours (depending on your PC or server configuration), your build should complete successfully. 

### Troubleshooting
You may encounter errors during the build process. Seek help from ROM support groups or dedicated builders' groups if needed.

---

I hope you find this tutorial helpful! If you have any questions or need further assistance, feel free to reach out.
