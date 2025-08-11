---
title: Certificate printing with dynamic text
date: 2021-11-07
published: true
tags: ['NodeJs', 'Puppeteer']
canonical_url: false
description: "Certificate generation with web technologies"
---

I was approached with the requirement of printing marriage certificate by the temple authorities where community mass marriages are held twice every year. This post is walk through of how i built three separate mini projects to achieve this requirement, initially with no back up and then with backup in a google sheet where the data is collected in a google form. The web dashboard built with this project has a `print` button that integrates with an express app and uses puppeteer to generate PDF with the passed in dynamic data.

When i was given this requirement i wasnt sure how to go about building it, but then i decided to take the simplest approach of building a simple vue2 application that has a form for various text that has to be displayed over the certificate like the `groom name`, `groom address`, `bride name` and `bride address`. I split the address into multiple form input so that i dont have to deal with line breaks. The background image for the certificate is also embedded in the page for preview, as soon the user enters the name or address, it appears on the certificate positioned by absolute positioning.

Now if the user tries to use the print option in the browser, the form elements along with the image shows up, this can be prevented by using `@media print { }` media query and then setting the `display` property to `none` on the elements that dont need to be on the print. I used the `@page` css variable to remove the header and footer by setting the `margin` property value to `0`.

The user flow is pretty simple, enter the data in the form, preview if the entered data is right(displays over the image) and then use the `print` option given by the browser.

This can be tried on the following site: [marriage certificate](https://marriagecertificate-perne.netlify.app).

This is the link to the github repo: [marriage certificate repo](https://github.com/RakshithNM/marriagecertificate/tree/master)

With this approach everything works just as fine but the only problem is backup, there is no way to keep track of the marriages and a google form was setup to address this. With google form, the data entered can be collected in a google sheet, so the problem of backup is solved.

With the form and sheet in place, the temple authorities that generate the certificate using the [marriage certificate](https://marriagecertificate-perne.netlify.app) site will have to enter the data manually from the sheet. To solve this, i built a dashboard that lists the data from sheets using the demo at [g-sheets-api](https://github.com/bpk68/g-sheets-api).

This can be tried on the following url: [marriage certificate dashboard](https://pernekshethracertificates.netlify.app/list/index.html)

This is the link to the github repo: [marriage certificate dashboard repo](https://github.com/RakshithNM/sheets-api-javascript-client)

The purpose of building the dashboard was to automatically trigger a generate a PDF and then print it. To solve this issue, i built an express app that runs puppeteer, fills the form on already built on [marriage certificate](https://marriagecertificate-perne.netlify.app) and then returns the generate PDF and opens in the browser PDF viewer. This is the link to the puppeteer pdf generation express app repo [pupp eteer pdf generation](https://github.com/RakshithNM/puppeteer-pdf-generation)

A `print` button was added to every row in the dashboard with the data from the sheets and upon clicking it, the data of the row in the sheet is sent to the express app where it runs puppeteer fills the form and returns the PDF to the client. So now there is no manually intervention required from the temple authorities in entering the input. In case there are any correction requirred to the recieved data, the google sheet that collects data can be edited.

This can be used to generate certificates with any base image so can be used to generate other types of certificates with dynamic text not just marriage certificate.
