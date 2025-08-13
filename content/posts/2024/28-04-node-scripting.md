---
title: Automating HTML generation using NodeJs
date: 2024-04-28
published: true
tags: ['NodeJs', 'Automation', 'HTML', 'StaticSite']
description: "Generating static sites from HTML template using NodeJs for better development experience"
---

Few months ago I was approached to build a website for the Oushadhavana
initiative by the Perne temple, this article is a run down of how I built the
site.

![oushadhavana landing page](/images/posts/oushadhavana/main.png)

You can check the site at [Perne Oushadhavana](https://pernekshetra.com/oushadhavana).

The repo is [Perne kshetra repo](https://github.com/pernekshetra/perneMuchilotkshetra).

As you can see the main task was to display the images and description of the
different plants that are planted at the temple premises. The website is
deployed on github pages and we don't have a way to do some sort of server side
rendering and not generate multiple pages.

The natural solution that I arrived at was to just generate individual HTML
pages for each plant. This will be a cumbersome process if done for each plant
as the data for each plant is different.

The data for each plant was stored in Google sheet. I had to some how use that
data and generate HTML pages for each plant.

Since we can download a CSV version of the Google sheet, that is what I used and
converted it to JSON. Naturally the data to the sheet was entered in stages and
this got cumbersome soon to convert the CSV to JSON. This naturally was asking
to be automated.

This code converts the CSV to JSON and if an older data file exists deletes it
and puts the JSON data into the file. Now we have the data source required in
the format we need.

```js
import https from 'https';
import fs from "fs";
import Papa from "papaparse";

const csvFilePath = '../../oushadhavana.csv';
const csvData = fs.readFileSync(csvFilePath, 'utf8');

const tempJson = `../../temp-json.mjs`;

// Parse CSV and convert to JSON
Papa.parse(csvData, {
  header: true,
  complete: function(results) {
    // Convert results to JSON
    const data = `const plants = ${JSON.stringify(results.data)};\n\nexport default plants;
    `
    fs.writeFile(tempJson, data, (err) => {
      if (err) {
        console.error('Error creating file:', err);
      } else {
        console.log('File created successfully');
      }
    });
  }
});

const filePath = '../../data.mjs';

// Check if the file exists
fs.access(filePath, fs.constants.F_OK, (err) => {
  if (err) {
    console.error('File does not exist');
    return;
  }

  // File exists, so delete it
  fs.unlink(filePath, (err) => {
    if (err) {
      console.error('Error deleting file:', err);
      return;
    }
    console.log('File deleted successfully');

    const newFilePath = '../../data.mjs';

    fs.rename(tempJson, newFilePath, (err) => {
      if (err) {
        console.error('Error renaming file:', err);
        return;
      }
      console.log('File renamed successfully');
    });
  });
});
```
To display the different plant data I decided on using VueJs. The details page
is [here](https://github.com/pernekshetra/perneMuchilotkshetra/blob/main/oushadhavana/scripts/details.js)
and the listing page is [here](https://github.com/pernekshetra/perneMuchilotkshetra/blob/main/oushadhavana/scripts/listing.js)

I have used a template file that uses the Vue variables and tries to display the
different data. This file is copied to different individual files and is done
using the script below.

```js
import fs from 'fs';
import plants from '../data.mjs';

const pathOfFileToCopy = '../base.htmx';

for(const plant of plants) {
  const folderPath = `../${plant['Sanskrit Name'].toLowerCase().replace(/\s+/g, '_')}`;

  fs.stat(folderPath, (err, stats) => {
    if (err) {
      if (err.code === 'ENOENT') {
        fs.mkdir(folderPath, (err) => {
          if (err) {
            console.error('Error creating folder:', err);
            return;
          } else {

            fs.readFile(pathOfFileToCopy, 'utf8', (err, html) => {
              if (err) {
                console.error('Error reading file:', err);
                return;
              }

              const titleStart = html.indexOf('<title>');
              const titleEnd = html.indexOf('</title>');

              if (titleStart === -1 || titleEnd === -1) {
                console.error('Title tag not found in the HTML file');
                return;
              }

              html.substring(titleStart + 7, titleEnd);

              const newTitle = `${plant['Sanskrit Name']} Oushadhavana - Perne`;
              const updatedHtml = html.substring(0, titleStart + 7) + newTitle + html.substring(titleEnd);

              const filePath = `${folderPath}/index.html`;

              fs.writeFile(filePath, updatedHtml, (err) => {
                if (err) {
                  console.error('Error creating file:', err);
                } else {
                  console.log('File created successfully', filePath);
                }
              });
            });
          }
        });
      } else {
        console.error('Error checking folder:', err);
      }
    } else {
      if (stats.isDirectory()) {
        console.log('Folder exists', folderPath);
        return;
      } else {
        console.log('Path exists, but is not a folder');
        return;
      }
    }
  });
}
```
The base template only needs to changed when additional data needs to displayed
or designed has to be changed.

If there is any data change then, the process of conversion of CSV to JSON and
the process of generation of HTML files has to be done everytime. In this case
we will already have files of already generated HTML we need to delete it and
this is done using the script [here](https://github.com/pernekshetra/perneMuchilotkshetra/blob/main/oushadhavana/scripts/deletePlantsDirectory.mjs)

Since this website is deployed on Github pages and we don't want any cost
overhead in maintaining the task, this looked like the ideal way to go about
implementing the requirements.
