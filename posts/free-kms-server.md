因为自己开 VPS 要给虚拟机激活 Windows，所以搭了一个 KMS 服务器

> 推荐使用一键快速激活工具，[点击这里下载](https://git.zerodream.net/Akkariin/ZeroKMS/raw/branch/master/ZeroKMS.cmd)
>
> 打开后右键另存为到任意位置，然后双击运行即可使用

各位如果有需要也可以使用，以下是激活方法：

首先打开命令提示符，开始菜单 -> 输入 `cmd` -> 回车，然后输入以下命令进行激活：

```
slmgr /ipk <激活秘钥>
slmgr /skms s1.tcotp.cn
slmgr /ato
```

执行后大概需要十几秒钟的时间才会返回结果，可以打开计算机 -> 属性查看激活是否成功

也可以输入以下命令查询 KMS 到期时间，一般是 180 天之后，所以只需要半年激活一次即可

```
slmgr /xpr
```

以下是各种操作系统的激活密钥：

**Windows Server** **版本** **1809**

| 系统版本              | 激活密钥                  |
| ------------------------- | ----------------------------- |
| Windows Server 数据中心版 | 6NMRW-2C8FM-D24W7-TQWMY-CWH2D |
| Windows Server 标准版   | N2KJX-J94YW-TQVFB-DG9YT-724CC |

**Windows Server** **版本** **1803**

| 系统版本              | 激活密钥                  |
| ------------------------- | ----------------------------- |
| Windows Server 数据中心版 | 2HXDN-KRXHB-GPYC7-YCKFJ-7FVDG |
| Windows Server 标准版   | PTXN8-JFHJM-4WC78-MPCBR-9W4KR |

**Windows Server** **版本** **1709**

| 系统版本              | 激活密钥                  |
| ------------------------- | ----------------------------- |
| Windows Server 数据中心版 | 6Y6KB-N82V8-D8CQV-23MJW-BWTG6 |
| Windows Server 标准版 | DPCNP-XQFKJ-BJF7R-FRC8D-GF6G4 |

**Windows Server 2019**

| 系统版本                   | 激活密钥                    |
| ------------------------------ | ------------------------------- |
| Windows Server 2019 数据中心版 | WMDGN-G9PQG-XVVXX-R3X43-63DFG   |
| Windows Server 2019 标准版     | N69G4-B89J2-4G8F4-WWYCC-J464C   |
| Windows Server 2019 基础版 | WVDHN-86M7X-466 P 6-VHXV7-YY726 |

**Windows Server 2016**

| 系统版本                   | 激活密钥                  |
| ------------------------------ | ----------------------------- |
| Windows Server 2016 数据中心版 | CB7KF-BWN84-R7R2Y-793K2-8XDDG |
| Windows Server 2016 标准版   | WC2BQ-8NRM3-FDDYY-2BFGV-KHKQY |
| Windows Server 2016 基础版 | JCKRF-N37P4-C2D82-9YXRT-4M63B |

**Windows 10**

| 系统版本            | 激活密钥                  |
| ----------------------- | ----------------------------- |
| Windows 10 专业版       | W269N-WFGWX-YVC9B-4J6C9-T83GX |
| Windows 10 专业版 N     | MH37W-N47XK-V7XM9-C7227-GCQG9 |
| Windows 10 专业工作站   | NRG8B-VKK3Q-CXVCJ-9G2XF-6Q84J |
| Windows 10 专业工作站 N | 9FNHH-K3HBT-3W4TD-6383H-6XYWF |
| Windows 10 专业教育版   | 6TP4R-GNPTD-KYYHQ-7B7DP-J447Y |
| Windows 10 专业教育版 N | YVWGF-BXNMC-HTQYQ-CPQ99-66QFC |
| Windows 10 教育版       | NW6C2-QMPVW-D7KKK-3GKT6-VCFB2 |
| Windows 10 教育版 N     | 2WH4N-8QGBV-H22JP-CT43Q-MDWWJ |
| Windows 10 企业版       | NPPR9-FWDCX-D2C8J-H872K-2YT43 |
| Windows 10 企业版 N     | DPH2V-TTNVB-4X9Q3-TJR4H-KHJW4 |
| Windows 10 企业版 G     | YYVX9-NTFWV-6MDM3-9PT4T-4M68B |
| Windows 10 企业版 G N   | 44RPN-FTY23-9VTTB-MP9BX-T84FV |

**Windows 10 LTSC 2019**

| 系统版本                  | 激活密钥                  |
| ----------------------------- | ----------------------------- |
| Windows 10 企业版 LTSC 2019   | M7XTQ-FN8P6-TTKYV-9D4CC-J462D |
| Windows 10 企业版 N LTSC 2019 | 92NFX-8DJQP-P6BBQ-THF9C-7CG2H |

**Windows 10 LTSB 2016**

| 系统版本                  | 激活密钥                   |
| ----------------------------- | ------------------------------ |
| Windows 10 企业版 LTSB 2016   | DCPHK-NFMTC-H88MJ-PFHPY-QJ4BJ |
| Windows 10 企业版 N LTSB 2016 | QFFDN-GRT3P-VKWWX-X7T3R-8B639  |

**Windows 10 LTSB 2015**

| 系统版本                      | 激活密钥                  |
| --------------------------------- | ----------------------------- |
| Windows 10 企业版 LTSB 2015 | WNMTR-4C88C-JK8YV-HQ7T2-76DF9 |
| Windows 10 企业版 N LTSB 2015 | 2F77B-TNFGY-69QQF-B8YKP-D69TJ |

**Windows Server 2012 R2**

| 系统版本                           | 激活密钥                  |
| -------------------------------------- | ----------------------------- |
| Windows Server 2012 R2 标准版 | D2N9P-3P6X9-2R39C-7RTCD-MDVJX |
| Windows Server 2012 R2 数据中心版     | W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9 |
| Windows Server 2012 R2 基础版      | KNC87-3J2TX-XB4WP-VCPJV-M4FWM |

**Windows Server 2012**

| 系统版本                            | 激活密钥                  |
| --------------------------------------- | ----------------------------- |
| Windows Server 2012                     | BN3D2-R7TKB-3YPBD-8DRP2-27GG4 |
| Windows Server 2012 N                  | 8N2M2-HWPGY-7PGT9-HGDD8-GVGGY |
| Windows Server 2012 单语言版            | 2WN2H-YGCQR-KFX6K-CD6TF-84YXQ |
| Windows Server 2012 特定国家/地区版     | 4K36P-JN4VD-GDC6V-KDT89-DYFKP |
| Windows Server 2012 标准版 | XC9B7-NBPP2-83J2H-RHMBY-92BT4 |
| Windows Server 2012 MultiPoint 标准版 | HM7DN-YVMH3-46JC3-XYTG7-CYQJJ |
| Windows Server 2012 MultiPoint 专业版  | XNH6W-2V9GX-RGJ4K-Y8X6F-QGJ2G |
| Windows Server 2012 数据中心版         | 48HP8-DN98B-MYWDG-T2DCC-8W83P |

**Windows Server 2008 R2**

| 系统版本                                   | 激活密钥                   |
| ---------------------------------------------- | ------------------------------ |
| Windows Server 2008 R2 Web 版                  | 6TPJF-RBVHG-WBW2R-86QPH-6RTM4  |
| Windows Server 2008 R2 HPC 版                  | TT8MH-CG224-D3D7Q-498W2-9QCTX  |
| Windows Server 2008 R2 标准版                  | YC6KT-GKW9T-YTKYR-T4X34，R7VHC |
| Windows Server 2008 R2 企业版                  | 489J6-VHDMP-X63PK-3K798-CPX3Y  |
| Windows Server 2008 R2 数据中心                | 74YFP-3QFB3-KQT8W-PMXWJ-7M648  |
| Windows Server 2008 R2 Itanium 版 | GT63C-RJFQ3-4GMB6-BRFB9-CB83V  |

**Windows Server 2008**

| 系统版本                                 | 激活密钥                  |
| -------------------------------------------- | ----------------------------- |
| Windows Server 2008 Web 版            | WYR28-R7TFJ-3X2YQ-YCY4H-M249D |
| Windows Server 2008 标准版        | TM24T-X9RMF-VWXK6-X8JC9-BFGM2 |
| Windows Server 2008 标准版（无 Hyper-V） | W7VD6-7JFBR-RX26B-YKQ3Y-6FFFJ |
| Windows Server 2008 企业版                   | YQGMW-MPWTJ-34KDK-48M3W-X4Q6V |
| Windows Server 2008 企业版（无 Hyper-V） | 39BXF-X8Q23-P2WWT-38T2F-G3FPG |
| Windows Server 2008 HPC 版                   | RCTX3-KWVHP-BR6TB-RB6DM-6X7HP |
| Windows Server 2008 数据中心版              | 7M67G-PC374-GR742-YH8V4-TCBY3 |
| Windows Server 2008 数据中心版（无 Hyper-V） | 22XQ2-VRXRG-P8D42-K34TD-G3QQC |
| Windows Server 2008 Itanium 版 | 4DWFP-JF3DJ-B7DTH-78FJB-PDRHK |

**Windows 8.1**

| 系统版本         | 激活密钥                  |
| -------------------- | ----------------------------- |
| Windows 8.1 专业版   | GCRJD-8NW9H-F2CDX-CCM8D-9D6T9 |
| Windows 8.1 专业版 N | HMCNV-VVBFX-7HMBH-CTY9B-B4FXY |
| Windows 8.1 企业版   | MHF9N-XY6XB-WVXMC-BTDCT-MKKG7 |
| Windows 8.1 企业版 N | TT4HM-HN7YT-62K67-RGRQJ-JFFXW |

**Windows 8**

| 系统版本       | 激活密钥                  |
| ------------------ | ----------------------------- |
| Windows 8 专业版   | NG4HW-VH26C-733KW-K6F98-J8CK4 |
| Windows 8 专业版 N | XCVCF-2NXM9-723PB-MHCB7-2RYQQ |
| Windows 8 企业版   | 32JNW-9KQ84-P47T8-D8GGY-CWCK7 |
| Windows 8 企业版 N | JMNMF-RHW7P-DMY6X-RF3DR-X2BQT |

**Windows 7**

| 系统版本       | 激活密钥                  |
| ------------------ | ----------------------------- |
| Windows 7 专业版   | FJ82H-XT6CR-J8D7P-XQJJ2-GPDD4 |
| Windows 7 专业版 N | MRPKT-YTG23-K7D7T-X2JMM-QY7MG |
| Windows 7 专业版 E | W82YF-2Q76Y-63HXB-FGJG9-GF7QX |
| Windows7 企业版    | 33PXH-7Y6KF-2VJC9-XBBR8-HVTHH |
| Windows 7 企业版 N | YDRBP-3D83W-TY26F-D46B2-XCKRJ |
| Windows 7 企业版 E | C29WB-22CC8-VJ326-GHFJW-H9DH4 |
