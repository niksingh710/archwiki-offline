# ArchWiki Offline Access Script

**ArchWiki Offline Access Script** is a powerful tool to fetch and search the ArchWiki documentation offline right from your terminal. It relies on the `arch-wiki-docs` package to provide you with a seamless experience of browsing and troubleshooting Arch Linux related topics.

## Features

- **Offline Access**: Browse ArchWiki documentation without requiring an active internet connection.

- **Flexible Display Modes**: Choose between `rofi`, `dmenu`, or `fzf` for listing and selecting ArchWiki topics.

- **Customizable Opening Method**: Open links using `xdg-open`, `firefox`, `chromium`, `w3m`, or your preferred application.
Absolutely, here's the revised installation section with the "manual" method included:

## Installation

### Manual Installation
1. Install the arch-wiki-docs package using your package manager:
  ```bash
  yay -S arch-wiki-docs
  ```

2. Clone this repository:

    ```bash
    git clone https://github.com/niksingh710/archwiki-offline.git
    cd archwiki-offline
    ```

3. Make the script executable:

    ```bash
    chmod +x archwiki
    ```

### Using AUR Package (Recommended)
1. Install the `archwiki-offline` package from AUR:

    ```bash
    yay -S archwiki-offline
    ```

Using the AUR package is the recommended method as it takes care of dependencies and provides a smoother installation experience.

## Usage

```bash
./archwiki [FLAGS]
```

**Flags**:

- `-h`: Display help information.
- `-d`: Disown the process. (Does not keep the terminal hanging after opening the file in a browser)
- `-m MODE`: Select the display mode (`rofi`, `dmenu`, or `fzf`).
- `-o OPENER`: Specify the opening method for links (`xdg-open`, `firefox`, `chromium`, `w3m`, etc.). Default is `xdg-open`.

## Tips

### Example with fzf

For a seamless experience with `fzf`, consider creating a wrapper script that formats the page titles for better readability and uses `w3m` to display a preview of the selected page:

```bash
#!/bin/bash

# Custom script for using fzf with ArchWiki offline access
# Replaces spaces in the selected topic with underscores and opens the corresponding HTML file in w3m for preview

# Usage: ./fzf_archwiki.sh "Selected ArchWiki Topic"

# Replace spaces with underscores
selected_topic=$(echo "$1" | sed 's/ /_/g')

# Open the HTML file using w3m for preview
w3m /usr/share/doc/arch-wiki/html/en/$selected_topic.html
```

You can save this script as `fzf_archwiki.sh`, make it executable (`chmod +x fzf_archwiki.sh`), and use it along with your main script. Here's how you can use it:

```bash
archwiki-offline -m "fzf --preview './fzf_archwiki.sh {}'"
```

With this script, the selected ArchWiki topic will be passed to the `fzf_archwiki.sh` script, which will replace spaces with underscores and open the corresponding HTML file using `w3m` for a preview.

Remember to adjust file paths and names according to your actual setup if needed.
This will allow you to preview the selected topic in the terminal itself before opening it in your browser.

### Dark Mode in Browser

If you prefer using a browser to preview the ArchWiki files instead of `w3m`, you can take advantage of the [Dark Reader](https://darkreader.org/) extension to enable dark mode for the ArchWiki pages. However, there's a catch: when the pages are fetched from the system in offline mode, Dark Reader might not automatically apply the dark theme. To ensure it works seamlessly, follow the instructions below:

#### For Chrome

1. Open a new tab and enter `chrome://extensions` in the address bar.
2. Locate "Dark Reader" in the extensions list and click on it.
3. Enable the option "Allow access to file URLs."

#### For Firefox

1. Type `about:config` in the Firefox address bar and press Enter.
2. In the search bar, enter `security.fileuri.strict_origin_policy`.
3. Double-click on the entry to set it to `false`.
4. Restart Firefox to apply the changes.

These adjustments will ensure that Dark Reader can successfully apply dark mode to the offline ArchWiki pages. If you encounter any issues or have further questions, feel free to create an issue on the [GitHub repository](https://github.com/niksingh710/archwiki-offline). You can also refer to [this issue on Dark Reader](https://github.com/darkreader/darkreader/issues/475) for more information.

This enhancement will provide users with an option to enjoy the ArchWiki pages in dark mode when using a browser for previewing.
## Contribution

Feel free to contribute to this script by opening issues or submitting pull requests on the [GitHub repository](https://github.com/niksingh710/archwiki-offline). Your contributions will be highly appreciated.


## Acknowledgements

This project is made possible by the amazing [`arch-wiki-docs`](https://github.com/lahwaacz/arch-wiki-docs) project, which provides the backbone for offline ArchWiki access. A big thank you to the creators and maintainers of this tool for their dedication to the Arch Linux community.

Special thanks to [Lahwaacz](https://github.com/lahwaacz) for developing and maintaining `arch-wiki-docs`. Your work has significantly enriched the Arch Linux experience for users like me.

Without the invaluable efforts put into `arch-wiki-docs`, this project wouldn't have been possible. Thank you!

---

**Note:** This project is not affiliated with or endorsed by `arch-wiki-docs`. It simply builds upon the functionality provided by that project to offer a more streamlined offline ArchWiki access experience.

## License

This project is licensed under the [MIT License](LICENSE).

