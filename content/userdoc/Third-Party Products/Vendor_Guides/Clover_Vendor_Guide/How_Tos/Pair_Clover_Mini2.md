---
title: "How to pair Clover Mini 2 to POS PRO"
date: 2023-03-29T07:26:00-05:00
draft: false
weight: 1
---

{{% notice warning %}}
This vendor guide is currently under construction and its contents should not be used until further notice.
{{% /notice %}}

- [Overview](#Overview)  
- [Configuring CHQ](#CHQ)  
- &nbsp;&nbsp;&nbsp;&nbsp;[Creating a payment method](#CreatingAPaymentMethod)  
- &nbsp;&nbsp;&nbsp;&nbsp;[Applying the payment method](#ApplyingThePaymentMethod)  
- [Configuring the Clover Mini 2](#CloverMini2)  
- [Configuring the iPad](#iPad)  
- [Pairing the iPad and Clover Mini 2](#PairingTheIPadAndMini)

---

## Overview {#Overview}

This topic describes how to pair a Clover Mini 2 to Teamwork POS PRO. The pairing occurs in three locations: **(1)** in CHQ, **(2)** on an iPad, and **(3)** on a Clover Mini 2.

## Configuring CHQ {#CHQ}

### Creating a payment method {#CreatingAPaymentMethod}

A *Credit Payment Method* needs to be created in CHQ.

Before creating the payment method, the CSM Team should be contacted to obtain the information needed to properly configure the payment method.

Once this information has been obtained, navigate to **CHQ** > **settings** > **sales** > **payment methods** and click on the **New** button to open the *new payment method* dialog box:

{{% gimg src="VG_Clover_V01.00/CHQ_NewPaymentMethod.jpg" title="CHQ: New Payment Method dialog" width="900px" %}}

Select **credit card** in the **payment type** combobox.

{{% gimg src="VG_Clover_V01.00/CHQ_Clover_CC_Dlg.jpg" title="CHQ: Clover Credit Card dialog" width="900px" %}}

In the **code** and **description** fields enter the payment method's name and description, respectively. Fill in the payment method's remaining configuration information which was obtained from the CSM Team.

Click the **save** button to save the payment method which will return you to the *payment methods* screen.

### Applying the payment method {#ApplyingThePaymentMethod}

The just created payment method can be applied from the *payment methods* screen by:
1. Selecting the just created payment method from the list using the method's name (supplied in the **code** field above).  
2. Clicking the **location settings** text button to open the *location settings* dialog box.

{{% gimg src="VG_Clover_V01.00/CHQ_LocationSettingsDlg.jpg" title="CHQ: Location Settings dialog" width="900px" %}}

For the desired location, double-click the **payment processing** column and select "Clover" from the displayed options.

Click the **save** button to save the information.

At this point we have created the payment method in CHQ.

## Configuring the Clover Mini 2 {#CloverMini2}

The POS Pro/Clover integration is a *Payment As A Service (PaaS)* semi-integration via the **Network Pay Display** (see the *Payments-As-A-Service* article in the *Overview* section for further information).

On the Clover device navigate to **More Tools** > **Network Pay Display**.

When opening the **Network Pay Display** for the first time it is necessary to do the **Initial Configuration**. This is done by tapping the *menu* icon (the three bars on the top let corner of the screen) and then tap **Settings** to display the *Clover Device Server* screen.

{{% gimg src="VG_Clover_V01.00/Mini2_CloverDeviceServer.jpg" title="Mini2: Clover Device Server" width="900px" %}}

Select (turn on) the **Server Is Secured**, **Enable Ping**, **Enable Pairing Screen** check boxes. For testing, select (turn on) the **Enable Development Certificate** check box. 

{{% notice warn %}}
The **Enable Development Certificate** checkbox should only be turned **ON** for *testing*. It should **ALWAYS** be **OFF** for *production*.
{{% /notice %}}

Tap the **Configure and Restart Server** button.

After configuring the server, tap the **Back** button to return to the main screen.

## Configuring the iPad {#iPad}

On the iPad navigate to the https://www.clover.com/v2/env_device_ca_certificate.der link to download the TEST certficate.

After tapping the link a pop up window will appear. On the iPad Tap **allow** and then navigate to **Settings** > **Profile Downloaded** and tap **Install** in multiple screens, and finally tap **Done**.

{{% gimg src="VG_Clover_V01.00/iPad_Settings.jpg" title="iPad: Settings" width="900px" %}}

{{% gimg src="VG_Clover_V01.00/iPad_SettingsPart2.jpg" title="iPad: Settings - Part2" width="900px" %}}

The certificate will now need to be *trusted* on the iPad. Navigate to **Settings** > **General** > **About** > **Certificate Trust Settings**. Set the **Clover Certificate Root** toggle to ON.

{{% gimg src="VG_Clover_V01.00/iPad_TrustSettings.jpg" title="iPad: Trust Settings"  width="450px" %}}

## Pairing the iPad and Mini 2 {#PairingTheIPadAndMini2}
Once the certificate has been installed on the iPad and the **Network Pay App** has been configured on the Clover Mini 2, the two devices need to be paired.

Have both devices side by side with **POS PRO** open on the iPad and the **Network Pay App** open on the Clover Mini 2.

On the Clover Mini 2 tap the **Start** button.

{{% gimg src="VG_Clover_V01.00/Mini2_NetworkPayDisplay.jpg" title="Mini 2: Network Pay Display" width="900px" %}}

The Clover Mini 2 will display either the Teamwork logo or a client logo.

{{% gimg src="VG_Clover_V01.00/Mini2_TeamworkLogo.jpg" title="Mini 2: Teamwork Logo" width="900px" %}}

On the iPad tap **More** (the three blue dots in the bottom right corner).

{{% gimg src="VG_Clover_V01.00/iPad_More.jpg" title="iPad: More" width="900px" %}}

Tap **Settings**.

{{% gimg src="VG_Clover_V01.00/iPad_Settings2.jpg" title="iPad: Settings" width="900px" %}}

Select **Payment Terminals** and tap **Edit Payment Terminal**.

{{% gimg src="VG_Clover_V01.00/iPad_EditPaymentTerminal.jpg" title="iPad: Edit Payment Terminal" width="900px" %}}

In the *Payment Terminals* dialog box select "Clover" in the **Payment Terminal Type** field and enter the IP address in the **IP Address** field.

{{% gimg src="VG_Clover_V01.00/iPad_PaymentTerminalDlg.jpg" title="iPad: Payment Terminal Dialog" width="900px" %}}

Then tap **Done**.

{{% gimg src="VG_Clover_V01.00/iPad_PaymentTerminalDlg_Done.jpg" title="iPad: Payment Terminal Dialog - Done" width="900px" %}}

At this point POS PRO will enter *working mode* and the Clover Mini 2 will prompt to enter the *admin code* (previously set up in Clover).

After entering the admin code, the Clover Mini 2 will ask for the pairing code which will be displayed in POS PRO.

{{% gimg src="VG_Clover_V01.00/Mini2_EnterPairingCode.jpg" title="Mini 2: Enter Pairing Code" width="900px" %}}

{{% gimg src="VG_Clover_V01.00/iPad_PairingCode.jpg" title="iPad: Pairing Code" width="900px" %}}

After the two devices are paired, sales are ready to be run.
