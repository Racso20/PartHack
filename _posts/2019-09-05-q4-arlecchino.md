---
title: "Hackaton Telefonica 2019 – Reto P4st3b1n"
author: "PartyHack"
header: 
  teaser: "/assets/images/ctf.png"
---



Este es un desafió de Crypto del CTF Organizado por Q4 el 31 de Agosto del 2019

En un archivo arlecchino.txt encontramos el siguiente texto

	QcO6biBuby4uLiBlc3RvIHJlY2llbiBjb21pZW56YS4uLgo4WWVXMmZxWEkybnRLNU5sRVlyMlBMV2Y1YV
	dDVUNQem96UkZQVWtHUFE4bWM1bnpydkZQNmJpdlI4ZnZKSDVFTlE1aThva3RmUE1ITEYzdHlRNWJpOHIz
	UWt3dlZQb044b09QYlBOOXU3SzFMZ2ZjUENESFB4SVkyTnE1QnhFZ2d6VVI3SG5jd25ZdjlkaHc4dXExR1
	dZc0tjTU1GV2Q5Q2xmYjRCQlcwZXZYdFVCVFdLT3Y3UVhBWngwZ1ZZT1Q3R0ZOQXlBejVPOUgxbWJXcFdG
	eTJmeXB5ZmZtZ2M0bkltajFsYXJmWGdEMDZtNzFkeDhhNUM0R2RRNWE0dEFLQXNtQzJuNVh0MlAxcWNqS1
	ZJYkN1dENCQTVVbjdBVFRjUThCa0VWdzFNcmVKNlVhbUJONjFzRGhQellKTjBXTm4yMUtSMW9XM2J0eVNE
	MGhVSUNTN0F6RDhuMDVsQXpRcE84NUg1NzFvcHlLZHdoNXd2djB0VmdqaHJBbmszT1FYa0pwVHhya0trNk
	NQM0JNTXRHbldKdG4zcFFPaE8zd3FaWVBVWDNOQ3RqRzMxdGpBUzZFcU42SWNiV1NQY2pXdTlWVnJrUnh1
	YkFBSzdyYk5jOHE4T09WUnl1ODh0RzdjTVlpSXNJQ3BZYUpkVkN4ZnRaNkpZRmtxQmNvUzQ4QllmaUFjWD
	dJdm9NUDRkSVJHQ1JZSHBYR3pFM0M1VUtFMWFrMjNta210Q3lQdHZxOU13dVNPSVM2OFh2azNJeUJEZEdq
	c0w4YXpyUk40RWpHR0k3Q055bHpKWnlqemJOVjZ6SzhZU1V5bGM5a1hDanFldk5HTHQ1NnMyWDB0Zk54bH
	N4OWxicU1XaXBQVUVIUUd2REM2bnNrM0dFOTNwSVdaTGJncm1iaUhBc0lxVUUxQWR6SjJpekUwaVdEdWs1
	RXlhZ2plRXZ3dFVQVzR4YWlxMGxyaXM2UkdZdXAzMW1IZnFmTnkwWFVLOGVqWkNBWDhMQUM3WU50elVycW
	dRdHdzWGp3QkNzazVid1JvMVJyU2wwa0ZlT3p4UlA3cWNBRTZlbkRBY3g1WFVjeGt2dzFqeTlmZU1icm42
	MUVoN3p2eUpYY1E2Y09HWlM4WjFXQm9yenZpZE1yakVxeUhINk5UU25qbFpCQjRtUEw4MW94SmkzZTVSdW
	hpc1lRU2hlODFIbEJMcGlrcHJhSVcxenBNVEFJa2tXSTZxQThRQ1ZvdVFzY0JtRUtvNFFPTm1DUDhpTkJK
	dWlKVVQySDVtQ0NJV1ZHV0M3c3FOT2RHcU9yNTZGaVp3azVsTDlnc2lwRUtnMGNKSU5xQk9jWnNTNjZ5UW
	JaVWZjUGNzYnFacnJzcWZObnRsa3ZySEs1OEQ2N1J6STh1RldpUTNvcWpNeWhNODVMd1ZkY1dxUDdvUWlQ
	MjBnZlVscUtSWG5venFySW96S0c0Q3pBaG5qMURiNDAxVTN4SXB1N1dO

Les recomiendo intentar solucionarlo antes de continuar. Para solucionarlo todo lo que necesitamos esta en CyberChef, fue un acierto de la organización tenerlo en local junto, para ustedes esta internet [https://gchq.github.io/CyberChef/](https://gchq.github.io/CyberChef/){:target="_blank"}

Lo primero que supongo la mayoría intento fue decodificar **base64** y se alegro de ver que funciono

	Aún no... esto recien comienza...
	8YeW2fqXI2ntK5NlEYr2PLWf5aWCUCPzozRFPUkGPQ8mc5nzrvFP6bivR8fvJH5ENQ5i8oktfPMHLF3tyQ
	5bi8r3QkwvVPoN8oOPbPN9u7K1LgfcPCDHPxIY2Nq5BxEggzUR7HncwnYv9dhw8uq1GWYsKcMMFWd9Clfb
	4BBW0evXtUBTWKOv7QXAZx0gVYOT7GFNAyAz5O9H1mbWpWFy2fypyffmgc4nImj1larfXgD06m71dx8a5C
	4GdQ5a4tAKAsmC2n5Xt2P1qcjKVIbCutCBA5Un7ATTcQ8BkEVw1MreJ6UamBN61sDhPzYJN0WNn21KR1oW
	3btySD0hUICS7AzD8n05lAzQpO85H571opyKdwh5wvv0tVgjhrAnk3OQXkJpTxrkKk6CP3BMMtGnWJtn3p
	QOhO3wqZYPUX3NCtjG31tjAS6EqN6IcbWSPcjWu9VVrkRxubAAK7rbNc8q8OOVRyu88tG7cMYiIsICpYaJ
	dVCxftZ6JYFkqBcoS48BYfiAcX7IvoMP4dIRGCRYHpXGzE3C5UKE1ak23mkmtCyPtvq9MwuSOIS68Xvk3I
	yBDdGjsL8azrRN4EjGGI7CNylzJZyjzbNV6zK8YSUylc9kXCjqevNGLt56s2X0tfNxlsx9lbqMWipPUEHQ
	GvDC6nsk3GE93pIWZLbgrmbiHAsIqUE1AdzJ2izE0iWDuk5EyagjeEvwtUPW4xaiq0lris6RGYup31mHfq
	fNy0XUK8ejZCAX8LAC7YNtzUrqgQtwsXjwBCsk5bwRo1RrSl0kFeOzxRP7qcAE6enDAcx5XUcxkvw1jy9f
	eMbrn61Eh7zvyJXcQ6cOGZS8Z1WBorzvidMrjEqyHH6NTSnjlZBB4mPL81oxJi3e5RuhisYQShe81HlBLp
	ikpraIW1zpMTAIkkWI6qA8QCVouQscBmEKo4QONmCP8iNBJuiJUT2H5mCCIWVGWC7sqNOdGqOr56FiZwk5
	lL9gsipEKg0cJINqBOcZsS66yQbZUfcPcsbqZrrsqfNntlkvrHK58D67RzI8uFWiQ3oqjMyhM85LwVdcWq
	P7oQiP20gfUlqKRXnozqrIozKG4CzAhnj1Db401U3xIpu7WN

Y continuamos quitando la primera linea y aplicando base64, pero esta vez nos llevo a un código con aspecto de binario, en el que perdimos un buen tiempo intentando saber que era. Hasta que volvimos atrás y probamos **base62** en CyberChef, obteniendo esto:

	Esto aún tiene para terminar.. sigue!
	24YQp8KKLgMNUC6R2gXetj6ga4CqjjVQ8Z1H8PpXnVyKapw6QZEnKtB1TGDyCEaWnW21uzNeEafsWpgdag
	E8CiJfDKFrhNiDo1LBFtxFUrSPt6hZtnbHNZQSVNYFa9gowc6iGkJRRndggdcsJSpQpM2JvytPfoRidAA3
	kj3jmQKv6eGSaxy48XmctgeMDg4UGW9ynPGTn7YzQPEcVHfoXkscWRh9zL97SNhy1b7K7HWpSnry2sBvSR
	m22F196pq1R43G8Ge2xD6iviuaqWZPGs8JqVGSFxMEuUF2W5nQRWCUWkKKi7Vhi5Y1u26t2REF7xVNrZWt
	oKnmg9Fs3TQYV79sHdrTPmcT6xQDvAUwoWmsApB4Rw5wLPaWT6So6tGiL9xSQxVxMwwLnB8mCxrCja3YTC
	Hhh1ebTWuJJbnkEHpN8nnUAvfcFgtDingz3aUWRDGVPBL1mnXyPCcBMy5QA9ywHyr2Z5taaTG8m17p7HCU
	PB4bAWdEqUmkZ35a7UzSZaTkLKLvtdXnMRDpCXjaL5Zxb3gkeXb5RX35sgp96w3fcYYXXtZVeVPCqFA8Au
	s2RthUTn1ZMrPdJaJbwMvBPktA8r97ofL3mjKPA6ZLcWuPFjigLst3Zmn6dfeGvkFAtcViDMPeCfRjficY
	AEAoSGj3dq8iDwjDiANz1LdQhSYmy7PmEiQcTRQWFpzrkRqgEWMnUAoAzi9XXvCZWkSHb7cy8UceSAQiWS
	DfYGrqXg9w1vrGmniqQpKxWmLmvgmA4cA21Pa66gBJaDFdtKKMac

En este punto ya intuimos que se trata de usar diferentes base, por lo que quitamos la primera linea y probamos, ahora es **base58**

	Aun te falta decodificar esto....
	KZQW233TEEQEMYLMORQSA4TFOBXWG3ZBEBYXKZJAMRUWGZJAMFUG64TBH4FDEKLVMQ3TASDAHAZCWPZJFE
	QTEYBJLA4ECZTSNFPSWPTUOFZTEX3DIY3DEJZ5MU5SWPSQKZXDEYBJLA4DEJZ5NA2SWPZBMFITERJ3NU6E
	CS2XNRRSWPSQLFXTCLBHNAWTEQSYNY4CWPZBLZIDERJ3NU6DCRK4KM4SWPZJFQRDERCIHU2DCRK4KM4SWP
	ZBM5JTESRCEFUDEJZ5NA3CWPSQKZXDESLENJTDAZBGGUVCWPTUOR2DERCIHU2ECS2XNRTCWPTVFERDEX3M
	JQ3DAZBGGUVCWPTVFERDEX3VKIZTASDAGUWSWPSZNBZTEZJBNVSEAM2AJNSCWPTVF4SDCR3HGQ2ECS2XNR
	TCWPSZLRXTELTEONUDCRK4KNTCWPZBMRJDELTEONUDCRK4JIWSWPTVEYQTCR2MEIYTEQSYMUYSWPTVEJ2T
	CR3HGQ2DCRK4JIXCWPSZLRXTESRCEFSTCRK4KY2CWPZKM4======

Quitamos la primera linea y esta vez es **base32**

	Vamos! Falta repoco! que dice ahora?
	2)ud70H`82+?))!2`)X8Afri_+>tqs2_cF62'=e;+>PVn2`)X82'=h5+?!aQ2E;m<AKWlc+&
	gt;PYo1,'h2BXn8+?!^P2E;m<1E\S9+?),"2DH=41E\S9+?!gS2J"!h2'=h6+>PVn2Idjf0d&
	;5*+>ttt2DH=4AKWlf+>u)"2_lL60d&5*+>u)"2_uR30H`5+>Yhs2e!md@3@Kd+>
	;u/$1Gg44AKWlf+>Y\o2.dsh1E\Sf+?!dR2.dsh1E\J-+>u&!1GL"12BXe1+>u"u1Gg44
	1E\J.+>Y\o2J"!e1E\V4+?*g

ahora **base85**

	59 20 65 73 74 6f 20 61 71 75 69 20 74 65 72 6d 69 6e 61 21 20 46 65 6c 69
	63 69 74 61 63 69 6f 6e 65 73 20 6c 61 20 62 61 6e 64 65 72 61 20 65 73 20
	51 34 7b 4a 75 67 34 6e 64 30 5f 63 6f 6e 5f 63 30 64 31 66 31 63 34 63 31
	30 6e 33 73 7d

Esto parece **hexadecimal**, y por fin tenemos la flag.
	
	Y esto aqui termina! Felicitaciones la bandera es Q4{Jug4nd0_con_c0d1f1c4c10n3s}
