# Wireless and mobile Security

Practical guide to introduce wireless and mobile technologies, and their vulnerabilities

![GitHub last commit](https://img.shields.io/github/last-commit/Skeptical-Security/wireless_mobile_security?label=last%20update%3A)

## Common wireless technologies

"Wireless" is a very broad term that covers a large range of techniques, devices, and situations. However, people usually refer to **WiFi** and **Bluetooth**.

These wireless connections are easy to setup and use, but there are some important limits to know.

### Wi-Fi in very short

WiFi or "Wireless Fidelity" is a technology used to provide Internet access to multiples devices without physical cables. The router is connected to Internet through a wired connection, but the connected devices receive and transmit data through radio waves, which are electromagnetic signals with a specific frequency (e.g., 2.4 GHz vs. 5 GHz).

Many electronic devices have a built-in WiFi adapter to exchange data with the router using the right protocol ([IEEE](https://en.wikipedia.org/wiki/Institute_of_Electrical_and_Electronics_Engineers) standards). 

Although, the quality of the connection can be affected by the number of connected devices or the distance to the router. Besides, interferences happen frequently (e.g., in high density environments).

WiFi has built-in security mechanisms to avoid unauthorized access to data, but there are documented vulnerabilities and attacks.

### Tethering in very short

Roughly speaking, the idea is to tether a device to another device that is connected to internet, for example, a smartphone or a laptop. In other words, it can consist of sharing the Internet access through a WiFi network or pairing devices with Bluetooth.

You may read similar terms like "mobile hotspot" or "mobile internet sharing."

It's often used as an alternative solution when the ISP or the Internet box is down or too slow. It's also not uncommon during events and conferences, when there's no router available.

It's convenient but has some cons. For example, it may consume lots of data, so it's probably better to use it as a last resort to avoid extra charges.

### Bluetooth in very short

Like WiFi, Bluetooth allows exchanging data over short distances without cables using radio waves. This protocol is meant for data transfer and has security mechanisms to protect its users.

However, there are important differences in speed and power consumption. You will likely choose WiFi for internet connectivity, as it has a longer range and a better speed overall.

You might even find that WiFi has a stronger encryption and better authentication mechanisms.

People usually prefer Bluetooth to connect low-power devices, such as headphones, to their smartphones. Still, it might also be used to tether Internet access.

### Bluetooth Low Energy (BLE)

This technology is now pretty much everywhere, and the associated vulnerabilities affect a large range of products. There are documented attacks (e.g., on BLE-based proximity authentication), and BLE sniffing is cheap.

As the name suggests, it's based on Bluetooth, but focuses low power. It's best suited for limited amounts of data, and is particularly useful for small IoT devices, like sensors or tags that do not have lots of battery power.

The trick is possible because those devices remain asleep the majority of the time, and only communicate for a few seconds.

## Common attacks and vulnerabilities

It's essential to list common attacks, again and again, as there are POCs (proofs of concept), open-source utilities, and even step-by-step demos in video available publicly, which lowers the barrier to entry for attackers significantly.

While the techniques are constantly evolving, here are some scenarios.

### WiFi attacks

#### The Preferred Network List

Every time you connect to new WiFi access points, your cellphone will store this information. **Your device will broadcast the full list of your recently stored access points, if you have enabled WiFi**.

Some manufacturers do not use that crazy old approach and leverage generic probes, but not all. Note that it's easy to use the word "crazy" now, but this is how the technology works. It yells very loud to see if a connection is available, and many routers do pretty much the same.

To avoid that bad situation, use the "forget this network" functionality to remove your previous connections, which means removing all previous access points. It can be a bit tedious, but it does improve your privacy and security.

If you don't need WiFi, then **shut it down**!

#### Man-in-the-middle (MitM) attacks 

The communication between two devices connected to the same WiFi network may be intercepted and modified to steal confidential data or inject malicious payloads.

#### Rogue access point

Fake WiFi access points can mimic the legitimate ones and trick users into giving their credentials and many other sensitive data.

#### Weak encryption 

WiFi security has been constantly improving over the past years, but older versions of the protocol are still available on some Internet Boxes, which can result in MitM attacks because of weak encryption.

Use the latest standard. At the time of writing, WPA 2 or WPA 3 are fine, but not WPA or WEP.

#### Password cracking

If the WiFi network relies on a weak password, attackers will gain unauthorized access, as they will attempt to crack it anyway.

#### Denial-of-service (DoS)

It's possible to flood a device with connection requests or data packets to crash it or deny its access.

There are documented techniques such as **Deauth** (sending deauthenticating packets to prevent the device from reconnecting) or **jamming** (~ generating radio frequency interferences).

### Bluetooth attacks

Most of the time, adversaries will enumerate nearby Bluetooth devices that are **discoverable** to find weaknesses and attack.

#### Bluejacking

Bluetooth Hijacking consists of sending unsolicited messages to a device to annoy the victims or attack them with social engineering techniques.

Although, most modern devices have built-in security to block such attempts efficiently.

#### Bluesnarfing

The attackers may find vulnerable devices and gain access to steal sensitive information like contact lists, SMS, emails, and other data like the IMEI (international mobile equipment identity).

In the worst-case scenario, adversaries can manage to divert incoming alls and messages to another device!

#### Bluebugging

Adversaries may take full control of a vulnerable device without the user's consent. They need to be quite close to the victims, but 10 meters is a relatively long distance that can correspond to various situations.

These attacks usually target the firmware of older Bluetooth devices to steal data, place phone calls, or send messages.

#### Denial-of-service (DoS)

Pretty much like WiFi DoS attacks (the general idea), but against Bluetooth-enabled devices. A typical example is the "Bluetooth ping flood attack."

Proximity is required too.

#### Eavesdropping

Attackers could intercept the communication between two vulnerable devices using a Bluetooth scanner or sniffer, allowing them to decode the Bluetooth signal and steal sensitive data.

There are related techniques like "car whispering" where adversaries target car radios and eavesdrop on conversations or phone calls made inside the car.

These attacks rely on legacy Bluetooth pairing or PIN to collect pairing frames and determine the corresponding secret keys.

#### BlueBorne hacks

[These hacks](https://www.armis.com/research/blueborne/) spread over the air (airborne) and don't even require attackers to pair with the targeted device, and can succeed even if the device is not in discoverable mode!

## Cellular attacks

### IMEI & IMSI in short

Roughly speaking the IMEI is the serial number on your phone and the IMSI is a nuique code associated with your subscription to a network provider. You ay google these acronyms to get the full description, but what is important for this security guide is what an attacker could do with such information.

Knowing the IMSI, it's theoretically possible to do the following:

* service availibility (e.g., call processing)
* SMS interception
* eavesdropping on voice calls
* location tracking

The IMEI may appear less critical, as it's not possible to steal your identity, and you can display the IMEI by dialing `*#06#` or simply browsing your phone settings. However, it's often used to track stolen devices and lock them out of the mobile network, so it's still important.

### State of the art

Cellphone networks are prone to various attacks, such as eavesdropping. It occurred to me that many products are still at risk, including those made by companies you may consider on top of their game...

There are public resources containing command injections and even actively exploited RCE (Remote Code Execution) related to 4G routers and their network layers. Security researchers have successfully retrieved IMSI and other critical data, like the location of the victims.

If you get errors when dialing numbers, and you have to make several attempts before you can make your calls, it's a red sign, and you should definitely contact your provider.

Such operations are more difficult to achieve than classic MitM attacks on public WiFi and non-HTTPS websites, but not so uncommon.

Be also extra careful when you turn your phone into a hotspot (~ modem), as the feature is meant to be a backup plan, not a primary functionality, and the hotspot can be detected quite easily.

### What is LTE?

Long Term Evolution (LTE) is the standard for most mobile communication (e.g., 4G LTE). Many passive (e.g., eavesdropping) and active LTE attacks are documented on Internet.

You will often find terms like Spoofing and Sniffing, but, IMHO, it's hard to find documentation about LTE Jamming and associated mitigations, which mostly depends on manufacturers and network providers.

In any case, LTE is supposed to provide stronger encryption and mutual authentication,and it does improve the standards, but, mobile phones seem to send various unprotected messages, regardless of the LTE station, including the potential evil ones.

### SIM card attacks

#### The SIM card has access to critical data

SIM (Subscriber Identity Module) cards can send messages on their own (e.g., probes). The SIM card is a computer system in itself, with a dedicated OS (e.g., SIM apps), that has network capabilities.

It is the primary point of entry for the network provider, and can even send requests to software, apps and other layers. The SIM can access to your current IMEI, even retrieve the previous phone IMEI. It can also get the IMSI, the current time, the text messages, the geographical location, the cell ID, and other valuable information, and there's nothing you can do about it.

I did not find many public documentations about SIM payloads, but some security researchers seem to have reversed the process, at least, partly. Any software/firmware update modifies an identifier called the IMSI EV, which is your IMSI followed by an alphanumeric code.

More generally, the SIM card can be used for advanced forensic analysis, and you'd be surprised how deep it can go.

#### SIM Swap

The attackers collect confidential information about you (e.g., through phishing or other social engineering attacks) and use them to contact your phone carrier. The goal is to impersonate you and force the company to transfer your line to another phone.

It's an efficient approach that do not require technical skills.

#### SIM Cloning

Basic physical access to your SIM card (e.g., theft) can allow an attacker to clone it. It's not easy to achieve, though, especially with the latest SIM cards, as the typical attack consits in putting the SIM in a specific equipment (e.g., special drives for the operation) and bombarding it with a specific software to Brute-Force its identification number.

The Ki, also known as the authentication key, is unique and encrypted. It's very hard to break, but not impossible, and experienced reversers (e.g., authorities but criminals as well) can sometimes break it in hours.

Such data are transmitted to the carrier to be compared with existing records in the database. There are multiple intermediary steps and other "temporary identifiers" for most operations, for example:

* TIMSI: Temporary Mobile Subscriber Identity
* GUTI: Globally Unique Temporary UE (User Equipment) Identity

This way, your cellphone does not expose your real identifiers all the time. Encryption makes reversing and forensic analysis way more complicated (~ longer), but with the right equipment, the motivation, and the required knowledge, some vulnerabilities can lead to the authentication key and the IMSI. Once you have that, you can theoretically duplicate the SIM.

#### The Simjacker attack

This attack usually aims to track the victim's location and exploits the S@T Browser, a SIM card library, to pass arbitrary commands using the SIM toolkit. 

According to researchers, millions of SIM cards were affected in 2019, involving various companies and countries. You might still have a vulnerable SIM card. 

[This SIM tester](https://github.com/srlabs/SIMtester) can be used to figured it out (not tested).

The SIM card has advanced capabilities from sending SMS and making calls to open URLs in a browser, and even establish a TCP connection. A mobile operator can even send special SMS called "OTA SMS" (binary SMS) for various purposes, like installing, updating, or removing applications.

### IMSI catcher and STINGRAY

Many people used to consider these devices unrealistic, perhaps like "pure science fiction", as it used bo be very expensive (thousands of dollars), but now attackers can build their own low-cost station for less than $1500. I won't explain it in details here, but the ultimate goal is to force the victim's phone to connect to a rogue "tower" (e.g., modified eNodeB).

Indeed, critical information like your IMSI are not transmitted all the time, but there are specific cases where it will be sent in clear text, for example:

* error recovery
* first time your connect your device to the network to claim that IMSI

These catchers are easily transportable. Unlike what your might read sometimes, it's not trivial to setup, but it's documented.

### Other attacks on cellphones

#### Crashing the modem

Various attacks attempt to bombard the modem processor to make it crash to ultimately take control of the device. An attacker can even send text messages or make calls from the targeted device after that, or get root access.

This would require specific conditions, like an outdated version of the OS, a vulnerable firmware, and other "details" but this approach is quite common.

#### SMiShing

These attacks are SMS-based phishing attacks where the victims receive unwanted SMS that contain links to phishing websites or malicious instructions to steal confidential information.

As the vast majority of smartphones are constantly connected to Internet, it's easy to click on these links. Some manufacturers have even started to remove all hyperlinks from SMS when you enable the security mode.

#### SMS Spoofing

Some attacks aim to impersonate a trusted source, like your bank, the police or the government. Various hacks and even legitimate platforms allow modifying the source name, but if you open the SMS details, you'll see it's a fraud.

#### Vishing

These are scams over the phone, using voice email, or VoIP (voice over IP).

#### Spoofed calls

In this scenario, the attacker can impersonate almost any cell number. There are now online platforms and Android/iOS applications that can make spoofed calls.

Why? Because it's not illegal! The scam is illegal, but not to make somebody believe you are someone else.

Note that attackers can use other approach, like these ones:

* using a burner phone number
* spoofing a caller ID while using a "real" number

There are free (or very cheap) apps for that too.

## How to protect wireless connections

### Bad approaches to avoid (IMHO)

While some articles may beg to differ, the following techniques aren't valuable **in a security perspective**.

#### Hidden SSIDs

WiFi settings allows "hiding" your Service Set IDentifier (SSID), but this information will be sent unencrypted during the negotiation process anyway.

If you suspect someone is trying to hack your connection, he will likely use a sniffer or a traffic monitoring software to discover your SSID.

#### MAC Address Filtering

Each device has a MAC address. It's possible to configure the router to whitelist specific MAC addresses, which seems a good idea, at first sight, but there are two major issues:

1. Your MAC address is sent along with network packets to ensure everything is delivered correctly
2. Cybercriminals can spoof whitelisted MAC addresses (e.g., using SMAC)

In a nutshell, **it's not a security feature**.

Although, it should be noted that some manufacturers now randomize MAC addresses, which improves both security and privacy, but it's unlikely old models have that capability.

### 9 effective mitigations

* keep devices and apps up-to-date
* use long and random passwords to secure access
* use robust encryption: use the latest security protocols (WPA2-AES, WPA 3)
* be cautious when pairing devices with unfamiliar devices
* read the specs carefully before buying cheap accessories or devices, and ensure they are built with the latest standards, especially for Bluetooth
* check the firmware against known CVEs for your model
* use firewalls and monitor your network for unusual traffic patterns (in corporate environments, you can also leverage network segmentation and intrusion detection systems)
* don't let your devices discoverable when not in use
* deactivate **unnecessary** network services and protocols

### Underrated strategies

#### Use a safe location

If the device holds sensitive data (e.g., credit cards, confidential documents), then keep it in a secure location.

Although, it might be problematic in real-world conditions, as people use smartphones for everything and anything, from entertainment to payments and administrative procedures.

To another perspective, it's essential to pair devices in a safe location, as some attacks specifically target the first connection to intercept data and forge security keys.

#### Disable WPS

The WiFi Protected Setup can allow an attacker to access to the wireless network without entering any password. You should turn it off.

Otherwise, anyone who has physical access to the router can get on the network.

#### Set rate limits

Some routers allow to prioritize specific traffic (e.g., WMM) and allocate bandwidth to a restricted list of devices and applications.

#### Pen-test your connection

We won't see pen-testing in details here, as this term is quite broad, but the idea with wireless pen-testing is to test wireless networks against known attacks regularly.

It's not highly expensive to create a rogue access point and a phishing page to see if the employees fall into the trap and give their credentials. You can leverage products like the [Wi-Fi Pineapple](https://www.wifipineapple.com/pages/software) to ease the setup.

Pen-testing distributions like Kali Linux also have pre-packaged utilities to sniff and hack wireless connections, starting with [detecting Hidden SSIDs](https://www.youtube.com/watch?v=7mQHmOZyY0Y&ab_channel=Packt).

## How to protect cellular connections

### Radical approaches that work

These options may be extreme and expensive depending on your country:

* use pre-paid SIM cards
* use an international SIM (roaming)
* remove the SIM from the phone when you don't use it
* buy products that allow disabling the SIM without removing it (pretty hard to find, though)
* use a data-only SIM: some plans do not include SMS, phone calls, and other classic mobile capabilities

### Other options are limited 

In my experience, there are very few mitigations against advanced SIM card attacks, and you don't control the mobile network (e.g., SS7 channel, network vulnerability). For example, the company should block binary SMS and address known SIM vulnerabilities, but it's not your decision.

Anyone who might know your personal data (unfortunately, it's not highly difficult to get those details) should not be able to port your cell number to another SIM/carrier. This is a serious threat, especially if you use that number for 2FA!

Nevertheless, it's not a valid reason to give up, and you can still move to another carrier. 

Besides, you can take measures to slow down a potential attacker, like enabling 2FA on accounts that control your cell number whenever it's possible, or contacting your phone carrier if you suspect something weird.

Only give your cell number to people you trust. It's a critical data that is tied to your real identity, most of the time.

Security researchers would likely compartmentalize, and use different phone numbers for their activities, for example:

* 1 for their personal usage (family, friends)
* 1 for online accounts that only provide SMS-based 2FA
* 1 for a professional usage
* 1 for all online platforms that requires a phone number while it's not critical for the service (e.g., Google)

This approach can be time-consuming and will likely require extra money, but it works. For now, a few companies provides platforms to ease the pain and manage all your numbers in one place, but it's not for the standard user, to me.

Besides, you may look supsicious for some actors, including phone carriers, and ultimately authorities.

Still, if you find such platforms online, maybe give it a try. You'll support companies that do a tremendous job for global privacy and security.

### Don't use eSIMs, for now

eSIM or virtual SIM cards are convenient for many users. You can have several phone numbers associated, which removes the hassle of buying and carrying several devices.

You may use devices that support dual-SIM instead, but it's limited to 2 SIM cards, by definition.

You cannot remove them, which could be useful to track stolen devices. Although, this advantage can be use to track you, and the transfer between devices is not as simple as you might think, so if the device stops working, be patient...

In a nutshell, in its current form, an eSIM is not really the best option, and does not bring significant security enhancements.

## Other "not so uncommon" wireless technologies

While Wi-Fi and Bluetooth security may seem prevalent, Radio frequency identification (RFID), near field communication (NFC), and many other contactless technologies exist and have their own vulnerabilities.

Many systems rely on these technologies to store sensitive data, make payments, or unlock cars and hotel rooms. These information can be captured very discreetly, without the victim's knowledge or consent.

You can buy[^1] a [Flipper Zero](https://flipperzero.one/) and start hacking in the wild. This product is very comprehensive and costs around $200 (at the time of writing).

[^1]: The product is sold-out at the time of writing, and Joom, the official reseller, "does not ship to the United States" ^^

## Best resources for beginners and intermediates

* [Hacktricks: pentesting WiFi](https://book.hacktricks.xyz/generic-methodologies-and-resources/pentesting-wifi)
* [A brief history of Wi-Fi security protocols from "oh my, that’s bad" to WPA3](https://arstechnica.com/gadgets/2019/03/802-eleventy-who-goes-there-wpa3-wi-fi-security-and-what-came-before-it/)
* [How to Hack Bluetooth Devices: 5 Common Vulnerabilities](https://hackernoon.com/how-to-hack-bluetooth-devices-5-common-vulnerabilities-ng2537af)
* [Rogue - deploy Access Points during penetration testing](https://github.com/InfamousSYN/rogue)
* [SANS - Enterprise Wireless Network Audit](https://www.sans.org/media/score/checklists/EnterpriseWirelessNetworkAudit.pdf)
* [CISA: Securing Networks for WiFi](https://www.cisa.gov/uscert/sites/default/files/publications/A_Guide_to_Securing_Networks_for_Wi-Fi.pdf)
* [NIST: Guide to Bluetooth security](https://www.nist.gov/publications/guide-bluetooth-security-2)
