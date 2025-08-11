---
title: Psuedo localization tool
date: 2023-03-04
published: true
tags: ['DeveloperExperience', 'QualityAssurance', 'UIDesign']
description: "A tool to preview layout changes due to localization"
---

A software that is available in multiple languages is usually designed and developed in one language(usually english).
Once the developement is done of of a feature, all the finalised texts are translated by translators who are unaware
of the layout constraints in the design and no effort is made to make the translated strings more concise if the they don't sit well in the layout.
This can lead to broken layout, or too much white space while the product is presented in some languages.

# 🦆 Why?
A software product that supports multiple languages has the vulnerability of having its layout broken during each release as new text is added.
This tool attempts to aid developers find these issues during the developement process by trying to suggesting a alternative elongated strings
in psuedo localized format. It is important for developers to still make out what the original text was and this is taken care by this tool.

# 🐈 How does "depslo" solve the problem?
The tool tries to mitigate those problems by performing psuedo localization of english sentences.

The developers can hit the endpoint with the JSON of translations in english and get back the psuedo localized JSON of all the strings.
The developers can use the command line utility to pass an entire JSON file that has english translations(see test/cli/test.json)
and get back Psuedo Localized files for all keys.

More details [here](https://github.com/RakshithNM/depslo/blob/main/README.md)
