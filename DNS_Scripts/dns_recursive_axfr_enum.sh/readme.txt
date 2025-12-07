#!/usr/bin/env bash
#
# dns_recursive_axfr_enum.sh
#
# Author: Vadym
# AI-assisted development
#
# Description:
#   Recursive DNS zone-transfer enumerator designed to automate AXFR-based
#   reconnaissance and discovery of misconfigured or delegated DNS subzones.
#
#   The script performs an AXFR transfer on the main target domain, extracts
#   all hostnames that contain A records, and then attempts additional AXFR
#   transfers on each of those hostnames. Any discovered TXT records—
#   commonly used for metadata, flags, or hidden configuration details—are
#   collected into a dedicated output file.
#
# Purpose:
#   Some DNS infrastructures allow AXFR on subzones even when zone transfer
#   on the primary domain is restricted or partially filtered. Automating this
#   enumeration accelerates discovery of overlooked delegation or leakage.
#
# Workflow:
#   1. Perform initial AXFR on the main domain.
#   2. Extract all hostnames associated with A records.
#   3. For each hostname:
#        • Attempt secondary AXFR
#        • Extract TXT records if present
#   4. Save all results into structured output files.
#
# Ideal use cases:
#   • Penetration testing
#   • HTB Academy DNS exercises
#   • CTF challenges involving DNS misconfigurations
#   • Internal or external reconnaissance
#
# Output files:
#   axfr_<domain>.txt     – raw initial zone dump
#   zones.txt             – extracted hostnames with A records
#   txt_from_zones.txt    – TXT records gathered from recursive AXFR
