# markdown-cli
Quick script to generate a (Github flavoured) markdown file to HTML and open it in the default browser.

# Installation

Clone this repository.

Run the following:
```
composer install
npm install
```

Make sure the `md` file is executable (git may do this for you during clone):
```
chmod +x md
```

Make sure the `md` executable is somewhere in your PATH, e.g.:
```
cd /usr/local/bin
ln -s /path/to/location/of/md
```