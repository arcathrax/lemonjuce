# lemonjuce
## Description
This is my personal collection of notes and examples related to using JUCE. I created it as a way to keep track of useful information – things I often find myself needing but that are scattered across forums and other resources.  It's meant to be a quick reference for me, [arcathrax](https://github.com/arcathrax), so I don't have to hunt down the same solutions every time!

One thing I’ve found frustrating with the official JUCE tutorials is that they sometimes rely on custom classes defined in previous tutorials. It can be a bit of a surprise when you're trying to follow along and suddenly get errors because you haven't created those supporting classes yet! This documentation aims to provide more complete, self-contained examples whenever possible, or at least clearly indicate any dependencies on earlier tutorial content.

## Start your own docs server
### Installing the dependencies
First make sure, that you have the latest version of [python](https://www.python.org/) installed. Next, you need to install [mkdocs](https://www.mkdocs.org) via the pip package installer:

```bash
pip install mkdocs
```

And lastly, you should clone this repository and start the mkdocs server:

MacOS:
```bash
git clone https://github.com/arcathrax/lemonjuce.git
cd lemonjuce
mkdocs serve
```

Windows:
```bash
git clone https://github.com/arcathrax/lemonjuce.git
cd lemonjuce
python -m mkdocs serve
```

## Disclaimer
Please note that this documentation is not intended to replace the official JUCE tutorials. It's meant as a supplementary resource – an addition to the existing information available. My goal is simply to create another useful tool for those learning and working with JUCE.