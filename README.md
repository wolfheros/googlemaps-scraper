# Google Maps Scraper(Only tested on Windows 11 )
Scraper of Google Maps reviews. It is very simple tools to download reviews.

## Installation
Follow these steps to use the scraper:
- Install Python packages from requirements file,using pip:

         pip install -r requirements.txt
- Put your url link in the file ``urls.txt``, all you links should at ``Google Map Reviews`` page.

**Note**: Python >= 3.6 is required, but less than version 3.9 (include).

## Basic Usage
The scraper.py script needs two main parameters as input:
- `--i`: input file name, containing a list of urls that point to Google Maps place reviews (default: _urls.txt_)
- `--N`: number of reviews to retrieve, starting from the most recent (default: 100)

Example:

  `python scraper.py --i .\urls.txt --N 50`

generates a csv file containing last 50 reviews of places present in _urls.txt_

In current implementation, the CSV file is handled as an external function, so if you want to change path and/or name of output file, you need to modify that function.

Additionally, other parameters can be provided:
- `--place`: boolean value that allows to scrape POI metadata instead of reviews (default: false)
- `--debug`: boolean value that allows to run the browser using the graphical interface (default: false)
- `--source`: boolean value that allows to store source URL as additional field in CSV (default: false)
- `--sort-by`: string value among most_relevant, newest, highest_rating or lowest_rating (default: newest), developed by @quaesito and that allows to change sorting behavior of reviews


## Monitoring functionality
The monitor.py script can be used to have an incremental scraper and override the limitation about the number of reviews that can be retrieved.
The only additional requirement is to install MongoDB on your laptop: you can find a detailed guide on the [official site](https://docs.mongodb.com/manual/installation/)

The script takes two input:
- `--i`: same as monitor.py script
- `--from-date`: string date in the format YYYY-MM-DD, gives the minimum date that the scraper tries to obtain

The main idea is to **periodically** run the script to obtain latest reviews: the scraper stores them in MongoDB up to get either the latest review of previous run or the day indicated in the input parameter.
