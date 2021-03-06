#Elektronické podepisování PDF pomocí certifikátu

Jako zdaleka nejvhodnější se zdá být program JSignPDF: https://github.com/kwart/jsignpdf
Program JSignPDF je aktivně vyvíjen, dá se použít z command line, má GUI na naklikání voleb, které se dají využít v command line, lze ho použít také jako plugin do OpenOffice a co je hlavní – funguje.
Nevýhodou je to, že je to program napsaný v Javě, ale to jsou všechny existující.
Instalace

Instalace a konfigurace JSignPDF
================================

1. Instalace JSignPDF
---------------------

<pre>
cd && \
wget http://sourceforge.net/projects/jsignpdf/files/stable/JSignPdf%201.6.1/JSignPdf-1.6.1.zip && \
unzip JSignPdf-1.6.1.zip && \
mv jsignpdf-1.6.1 jsignpdf && \
rm -f JSignPdf-1.6.1.zip && \
cd jsignpdf && \
echo Test funkcnosti javy spustenim helpu JSignPdf  && \
java -jar JSignPdf.jar -help
</pre>

2.	Instalace javy (pokud už není nainstalována)
------------------------------------------------

ideálně nějaká nová SUN/Oracle java, ta je otestovaná že funguje

3.	Export osobního certifikátu do formátu PKCS12 (.p12)
--------------------------------------------------------

Export certifikátu je možné provést například z Mozilla Firefox následujícím postupem:
![alt tag](https://github.com/kreuzwieser/jsignpdf-configuration/blob/master/export_certifikatu_z_firefox.png)

Vzhledem k tomu, že certifikát se většinou přes prohlížeč generuje, tak by v prohlížeči měl být dostupný.

V prostředí českých VŠ osobní certifikáty vydává CESNET ve spolupráci s TERENOU a tento certifikát je možné vystavit pomocí prohlížeče zde: https://tcs-p.cesnet.cz/confusa/process_csr.php

Zazálohovaný certifikát uložit do souboru ~/jsignpdf/keystore.p12. V exportovaném souboru musí být pouze jeden certifikát.

4.	konfigurace podepisování
----------------------------

A.	Předpokládáme, že ~/jsignpdf/keystore.p12 existuje z předchozího korku

B.	Do souboru do ~/jsignpdf/signature.png uložit nascanovaný podpis nebo stáhnout univerzální obrázek, který bude sloužit jako něco na co půjde v PDF kliknout. Například tento obrázek

<pre>
pushd ~/jsignpdf && \
wget https://raw.githubusercontent.com/kreuzwieser/jsignpdf-configuration/master/signature.png -O signature.png && \
popd
</pre>

C.	Stáhnout vzorovou konfiguraci pro JSignPDF do ~/.JSignPdf

<pre>
pushd ~ && \
wget https://github.com/kreuzwieser/jsignpdf-configuration/raw/master/.JSignPdf –O .JSignPdf && \
popd
</pre>

D.	Stáhnout bash script, který se ptá na heslo k úložišti certifikátu a podepíše všechny pdf v aktuálním adresáři. Umístit do adresáře v cestě.

<pre>
su - root -c "wget https://raw.githubusercontent.com/kreuzwieser/jsignpdf-configuration/master/sign_all_pdf -O /usr/bin/sign_all_pdf && chmod 555 /usr/bin/sign_all_pdf"
</pre>

Použití podpisového skriptu
===========================

Jen spustit "sign_all_pdf" a skript automaticky podepíše všechny PDF dokumenty v aktuálním adresáři.
