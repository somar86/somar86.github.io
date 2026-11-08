---
title: "DLIS to ANP Converter: Automating Data Delivery"
excerpt: "An app that converts DLIS files to ANP delivery format automatically, turning a week of back-and-forth across 20 people into seconds and increasing revenue 10x."
order: 3
toc: true
tags: [automation, software, data engineering]
---

**Role:** Designer and developer · **Organization:** SLB

## Overview

I built an application that converts **DLIS** well-log data into the **ANP** client delivery format. It automates **hundreds of delivery files every day** and finishes in **seconds** a job that used to take **about 20 people a week** of manual work and back-and-forth.

## The problem

Delivering processed well-log data to clients meant translating DLIS files (the industry-standard binary log format) into the required ANP deliverable. The process was manual, error-prone, and iterative: files moved between teams for checks and corrections, and every delivery cycle tied up people for days.

## Approach

- **Automated parsing** of DLIS files, including channels, frames, and metadata
- **Rule-based mapping and validation** to the ANP format, so errors are caught before delivery instead of in review loops
- **Batch processing** for hundreds of files per day with no manual intervention

## Impact

- **Turnaround cut from about 1 week to seconds**
- Freed about **20 people** from repetitive conversion and review work
- **Increased revenue by 10x** by removing the delivery bottleneck
