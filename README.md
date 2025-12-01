# NS300-opnsense-Status-no-carrier
NS300 Stormshield opnsense Status : no carrier

# SN300 "LEDs ON + no carrier" on brand-new unit – definitive fix
**Discovered by XTHOR – December 2025**

On a brand-new Stormshield SN300 bought for €60 (never powered on, original Stormshield SSD still inside) and after following the procedure at https://github.com/bmn-m/Stormshield-SN300-opnsense :

- All port LEDs light up  
- `ifconfig em0` → **status: no carrier** on every port, GUI IP unreachable  
- Serial console (`cu -l cuau1`) works, `port state 1-8 enable` accepted, LEDs stay on  
- promisc, switch reset, cable/PC/port changes → still nothing  
- Grok struggled for hours (and so did I) before giving up

**Solution (100 % tested & validated, previously unpublished anywhere – not on bmn-m GitHub, not on Stormshield/Netgate/OPNsense forums):**

1. Put back the **original Stormshield SSD** that came with the unit  
2. Boot it **once** (2 minutes is enough – no configuration needed)  
3. Power off → reinstall your OPNsense SSD  
4. Reboot → all ports go **status: active**, ping works, GUI appears instantly, Suricata IPS fully active

The official Stormshield firmware performs a **one-time initialization** of the switch ASIC (Broadcom/VIA) and PHYs that FreeBSD/OPNsense never does on first boot. Once done, the switch stays permanently unlocked.

**Result:** OPNsense 25.7, all 8 × 1 Gbit/s ports fully functional – perfect for a personal lab (<10 users).

**Discovered by XTHOR (xthr@protonmail.com) – December 2025**  
No glory, just facts for the next person who hits the same wall.

#SN300 #OPNsense #Homelab #Stormshield #NoCarrierFix
