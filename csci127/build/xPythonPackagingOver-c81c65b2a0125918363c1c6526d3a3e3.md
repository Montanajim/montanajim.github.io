# Python Application Packaging Tools

## Overview, Pricing, and URLs

This document presents a consolidated overview of major Python packaging tools, their costs, licenses, URLs, and practical notes suitable for classroom, textbook, and professional use.

------

## 1. Overview of Packaging Tools

Below is a summary of the most widely used tools for converting Python applications (including GUIs) into standalone executables or native installers.

### **cx_Freeze**

A free, open-source tool that works across Windows, macOS, and Linux. It bundles a Python script and its dependencies into a distributable executable directory. Very stable and ideal for teaching environments.

**URL:** https://pypi.org/project/cx-Freeze/

------

### **Nuitka**

A Python-to-C compiler that generates optimized binaries. It offers both free and commercial versions. The free version is suitable for typical course assignments, while the paid versions add advanced features.

**URL:** https://nuitka.net/

------

### **Briefcase (BeeWare Project)**

Creates native installers and application bundles for desktop and mobile platforms. Fully open-source. Excellent when you want applications that feel platform-native.

**URL:** https://beeware.org/briefcase/

------

### **py2exe**

A simple, Windows-only packaging solution. Useful for classrooms or labs where Windows is the standard environment.

**URL:** https://www.py2exe.org/

------

### **py2app**

The macOS equivalent of py2exe. Packages Python applications into macOS .app bundles.

**URL:** https://py2app.readthedocs.io/en/latest/

------

## 2. Pricing & Licensing Table

| Tool          | Price / License                                            | Notes                                                        |
| ------------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| **cx_Freeze** | Free, open source (PSF-derived license)                    | Ideal for teaching and student projects. Requires small license snippet in output per documentation. |
| **py2exe**    | Free, open source (MIT / MPL / X11)                        | Windows-only; very straightforward.                          |
| **py2app**    | Free, open source                                          | Mac-only; simple and stable.                                 |
| **Nuitka**    | Free core (Apache), Paid tiers: €250/yr, €400/yr, €1000/yr | Free version works for most student needs; paid tiers give extended features and support. |
| **Briefcase** | Free, open source (BSD-3-Clause)                           | Produces native installers; distribution to app stores may require respective account fees. |

------

## 3. When to Use Each Tool

- **cx_Freeze**: Best all-around free tool for desktop apps across platforms.
- **py2exe / py2app**: Great when students are working on a single OS environment.
- **Nuitka**: Use when you want compiled performance or to demonstrate how Python can become real binaries.
- **Briefcase**: Best for polished, platform-native installers and mobile distribution.

------

## 4. Additional Notes

- Packaging tools help students understand software distribution beyond the source-code level.
- Make sure students test executables on a fresh machine when possible.
- If building GUI apps (Tkinter, PyQt, PySide, Kivy), choose a packager that supports non-Python assets.
- Packaging is an excellent appendix or final chapter for a programming or GUI development textbook.