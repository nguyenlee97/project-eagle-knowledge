# Eagle hiện tại: tài nguyên theo đủ 1.687 ped ID

Ngày 14/10/2026. Đọc archive/index hiện tại, gồm ba NPC pilot. Đây là cấu hình/asset có sẵn, chưa phải danh sách model được quan sát cùng nạp trong gameplay.

RW MiB là độ dài root chunk khai báo; khi có phần đuôi khác zero, đây là lower bound. IMG MiB gồm sector padding. Texture mip không phải VRAM runtime. “Vùng” là tập ứng viên có sẵn, có overlap; chưa xác nhận spawn từng vùng. Slot có pedtype PLAYER1/2 không có nghĩa đang là nhân vật người chơi.

| ID | Model / TXD | Vai trò | RW MiB | IMG MiB | Tam giác | Vertex | Texture mip MiB | Texture / material | Vùng ứng viên | Ghi chú |
| ---: | --- | --- | ---: | ---: | ---: | ---: | ---: | --- | --- | --- |
| 0 | `null` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 7 | `male01` / `male01` | Dân thường | 0,103 | 0,105 | 1.209 | 1.166 | 0,016 | 1 / 1 | — | — |
| 9 | `BFORI` / `BFORI` | Dân thường | 0,203 | 0,205 | 1.072 | 1.024 | 0,125 | 1 / 2 | Carcer City, Los Santos | — |
| 10 | `BFOST` / `BFOST` | Dân thường | 0,188 | 0,191 | 1.022 | 753 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 11 | `VBFYCRP` / `VBFYCRP` | Dân thường | 0,205 | 0,209 | 1.133 | 1.055 | 0,125 | 1 / 1 | — | — |
| 12 | `BFYRI` / `BFYRI` | Dân thường | 0,247 | 0,250 | 1.143 | 1.253 | 0,156 | 2 / 3 | Vice City, Carcer City, Los Santos | P1 |
| 13 | `BFYST` / `BFYST` | Dân thường | 0,214 | 0,217 | 1.261 | 1.171 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 14 | `BMORI` / `bmori` | Dân thường | 0,192 | 0,195 | 1.048 | 822 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 15 | `BMOST` / `bmost` | Dân thường | 0,194 | 0,197 | 1.072 | 858 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 16 | `BMYAP` / `BMYAP` | Dân thường | 0,209 | 0,213 | 1.196 | 1.112 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 17 | `BMYBU` / `BMYBU` | Dân thường | 0,188 | 0,191 | 884 | 800 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 18 | `BMYBE` / `BMYBE` | Dân thường | 0,191 | 0,193 | 1.107 | 777 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 19 | `BMYDJ` / `BMYDJ` | Dân thường | 0,107 | 0,109 | 1.097 | 1.042 | 0,027 | 3 / 3 | Vice City, Carcer City, Los Santos | P1 |
| 20 | `BMYRI` / `BMYRI` | Dân thường | 0,202 | 0,205 | 1.179 | 963 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 21 | `BMYCR` / `BMYCR` | Criminal | 0,224 | 0,227 | 1.190 | 1.079 | 0,141 | 2 / 2 | Vice City, Carcer City, Los Santos | — |
| 22 | `BMYST` / `BMYST` | Dân thường | 0,098 | 0,102 | 1.181 | 1.074 | 0,016 | 1 / 1 | Carcer City, Los Santos | P1 |
| 23 | `WMYBMX` / `WMYBMX` | Dân thường | 0,209 | 0,211 | 1.199 | 1.101 | 0,125 | 1 / 1 | — | — |
| 24 | `WBDYG1` / `WBDYG1` | Dân thường | 0,245 | 0,248 | 1.852 | 1.568 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 25 | `WBDYG2` / `WBDYG2` | Dân thường | 0,247 | 0,250 | 1.920 | 1.594 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 26 | `WMYBP` / `WMYBP` | Dân thường | 0,212 | 0,215 | 1.218 | 1.154 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 27 | `WMYCON` / `WMYCON` | Dân thường | 0,208 | 0,211 | 1.246 | 1.066 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 28 | `BMYDRUG` / `BMYdrug` | Criminal | 0,226 | 0,229 | 1.153 | 1.145 | 0,141 | 2 / 2 | Vice City, Carcer City, Los Santos | — |
| 29 | `WMYDRUG` / `WMYdrug` | Criminal | 0,195 | 0,197 | 981 | 896 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 30 | `HMYDRUG` / `HMYdrug` | Criminal | 0,228 | 0,230 | 1.167 | 1.179 | 0,141 | 2 / 2 | Vice City, Carcer City, Los Santos | — |
| 31 | `DWFOLC` / `dwfolc` | Dân thường | 0,193 | 0,195 | 1.056 | 828 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 32 | `DWMOLC1` / `dwmolc1` | Dân thường | 0,189 | 0,191 | 944 | 796 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 33 | `DWMOLC2` / `dwmolc2` | Dân thường | 0,185 | 0,188 | 908 | 738 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 34 | `DWMYLC1` / `dwmylc1` | Dân thường | 0,193 | 0,195 | 1.021 | 845 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 35 | `HMOGAR` / `HMOgar` | Dân thường | 0,196 | 0,199 | 1.036 | 901 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 36 | `WMYGOL1` / `WMYgol1` | Dân thường | 0,194 | 0,197 | 1.004 | 866 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 37 | `WMYGOL2` / `WMYgol2` | Dân thường | 0,194 | 0,197 | 1.004 | 879 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 38 | `HFORI` / `hfori` | Dân thường | 0,192 | 0,195 | 1.050 | 824 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 39 | `HFOST` / `hfost` | Dân thường | 0,188 | 0,191 | 1.024 | 742 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 40 | `HFYRI` / `HFYRI` | Dân thường | 0,247 | 0,250 | 1.180 | 1.240 | 0,156 | 2 / 2 | Carcer City, Los Santos | P1 |
| 41 | `HFYST` / `HFYST` | Dân thường | 0,214 | 0,217 | 1.172 | 1.211 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | P1 |
| 43 | `HMORI` / `HMORI` | Dân thường | 0,192 | 0,195 | 988 | 841 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 44 | `HMOST` / `HMOST` | Dân thường | 0,196 | 0,199 | 1.080 | 884 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 45 | `HMYBE` / `HMYBE` | Dân thường | 0,191 | 0,193 | 1.107 | 777 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 46 | `HMYRI` / `HMYRI` | Dân thường | 0,245 | 0,248 | 1.222 | 1.179 | 0,156 | 2 / 2 | Carcer City, Los Santos | P1 |
| 47 | `HMYCR` / `HMYCR` | Criminal | 0,228 | 0,230 | 1.178 | 1.164 | 0,141 | 2 / 2 | Carcer City, Los Santos | — |
| 48 | `HMYST` / `HMYST` | Dân thường | 0,202 | 0,205 | 1.170 | 980 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 49 | `OMOKUNG` / `OMOkung` | Dân thường | 0,189 | 0,191 | 1.022 | 761 | 0,125 | 1 / 1 | — | — |
| 50 | `WMYMECH` / `WMYMECH` | Dân thường | 0,201 | 0,203 | 1.020 | 1.009 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 51 | `BMYMOUN` / `BMYMOUN` | Dân thường | 0,136 | 0,139 | 1.113 | 932 | 0,062 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 52 | `WMYMOUN` / `WMYMOUN` | Dân thường | 0,137 | 0,141 | 1.113 | 948 | 0,062 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 53 | `OFORI` / `OFORI` | Dân thường | 0,192 | 0,195 | 1.048 | 812 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 54 | `OFOST` / `OFOST` | Dân thường | 0,189 | 0,191 | 1.050 | 753 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 55 | `OFYRI` / `OFYRI` | Dân thường | 0,247 | 0,250 | 1.162 | 1.247 | 0,156 | 2 / 2 | Carcer City, Los Santos | — |
| 56 | `OFYST` / `OFYST` | Dân thường | 0,205 | 0,207 | 1.056 | 1.071 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 57 | `OMORI` / `OMORI` | Dân thường | 0,190 | 0,193 | 1.002 | 802 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 58 | `OMOST` / `OMOST` | Dân thường | 0,190 | 0,193 | 1.034 | 782 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | P1 |
| 59 | `OMYRI` / `OMYRI` | Dân thường | 0,212 | 0,215 | 1.241 | 1.147 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 60 | `OMYST` / `OMYST` | Dân thường | 0,203 | 0,207 | 1.106 | 1.025 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 61 | `WMYPLT` / `WMYPLT` | Dân thường | 0,194 | 0,197 | 990 | 884 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 62 | `WMOPJ` / `WMOpj` | Dân thường | 0,187 | 0,189 | 920 | 775 | 0,125 | 1 / 1 | — | — |
| 63 | `BFYPRO` / `BFYPRO` | Prostitute | 0,211 | 0,213 | 1.254 | 1.114 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 64 | `HFYPRO` / `HFYPRO` | Prostitute | 0,081 | 0,084 | 1.029 | 785 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 66 | `BMYPOL1` / `BMYpol1` | Dân thường | 0,250 | 0,252 | 1.960 | 1.628 | 0,125 | 1 / 1 | — | — |
| 67 | `BMYPOL2` / `BMYpol2` | Dân thường | 0,251 | 0,254 | 1.980 | 1.644 | 0,125 | 1 / 1 | — | — |
| 68 | `WMOPREA` / `WMOprea` | Dân thường | 0,191 | 0,193 | 954 | 837 | 0,125 | 1 / 1 | — | — |
| 69 | `SBFYST` / `sbfyst` | Dân thường | 0,205 | 0,209 | 1.093 | 1.068 | 0,125 | 1 / 1 | Carcer City | P1 |
| 70 | `WMOSCI` / `WMOsci` | Dân thường | 0,188 | 0,191 | 902 | 790 | 0,125 | 1 / 1 | — | — |
| 71 | `WMYSGRD` / `WMYSGRD` | Dân thường | 0,196 | 0,199 | 1.038 | 901 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 72 | `SWMYHP1` / `SWMYhp1` | Dân thường | 0,194 | 0,197 | 1.068 | 860 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | P1 |
| 73 | `SWMYHP2` / `SWMYhp2` | Dân thường | 0,194 | 0,195 | 1.048 | 848 | 0,125 | 1 / 1 | Vice City, Carcer City | P1 |
| 75 | `SWFOPRO` / `sWFOpro` | Prostitute | 0,191 | 0,193 | 1.006 | 816 | 0,125 | 1 / 1 | Carcer City | — |
| 76 | `WFYSTEW` / `WFYSTEW` | Dân thường | 0,223 | 0,225 | 1.237 | 1.365 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 77 | `SWMOTR1` / `sWMOtr1` | Dân thường | 0,192 | 0,195 | 938 | 856 | 0,125 | 1 / 1 | Carcer City | — |
| 78 | `WMOTR1` / `WMOTR1` | Dân thường | 0,189 | 0,191 | 943 | 790 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 79 | `BMOTR1` / `BMOTR1` | Dân thường | 0,082 | 0,084 | 956 | 839 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 80 | `VBMYBOX` / `VBMYbox` | Dân thường | 0,138 | 0,141 | 1.228 | 928 | 0,062 | 1 / 1 | — | — |
| 81 | `VWMYBOX` / `VWMYbox` | Dân thường | 0,138 | 0,141 | 1.228 | 928 | 0,062 | 1 / 1 | — | — |
| 82 | `VHMYELV` / `VHMYELV` | Dân thường | 0,210 | 0,213 | 1.293 | 1.084 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 83 | `VBMYELV` / `VBMYELV` | Dân thường | 0,205 | 0,209 | 1.245 | 1.011 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 84 | `VIMYELV` / `VIMYELV` | Dân thường | 0,210 | 0,213 | 1.293 | 1.093 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 85 | `VWFYPRO` / `VWFYPRO` | Prostitute | 0,190 | 0,193 | 957 | 820 | 0,125 | 1 / 1 | Carcer City | — |
| 87 | `VWFYST1` / `VWFYST1` | Dân thường | 0,252 | 0,256 | 1.982 | 1.675 | 0,125 | 1 / 1 | — | — |
| 88 | `WFORI` / `WFORI` | Dân thường | 0,190 | 0,193 | 1.030 | 788 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 89 | `WFOST` / `WFOST` | Dân thường | 0,188 | 0,191 | 1.026 | 743 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 90 | `WFYJG` / `WFYJG` | Dân thường | 0,206 | 0,209 | 1.160 | 1.056 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 91 | `WFYRI` / `WFYRI` | Dân thường | 0,245 | 0,248 | 1.118 | 1.215 | 0,156 | 2 / 2 | Vice City, Carcer City, Los Santos | P1 |
| 92 | `WFYRO` / `WFYRO` | Dân thường | 0,210 | 0,213 | 1.270 | 1.094 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 93 | `WFYST` / `WFYST` | Dân thường | 0,223 | 0,225 | 1.087 | 1.100 | 0,141 | 2 / 2 | Vice City, Carcer City, Los Santos | P1 |
| 94 | `WMORI` / `WMORI` | Dân thường | 0,192 | 0,195 | 1.052 | 812 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 95 | `WMOST` / `WMOST` | Dân thường | 0,194 | 0,197 | 1.036 | 858 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 96 | `WMYJG` / `WMYJG` | Dân thường | 0,148 | 0,150 | 1.252 | 1.113 | 0,062 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 97 | `WMYLG` / `WMYlG` | Dân thường | 0,148 | 0,150 | 1.234 | 1.126 | 0,062 | 1 / 1 | — | — |
| 98 | `WMYRI` / `WMYRI` | Dân thường | 0,240 | 0,242 | 1.167 | 1.102 | 0,156 | 2 / 2 | Carcer City, Los Santos | P1 |
| 99 | `WMYRO` / `WMYRO` | Dân thường | 0,202 | 0,205 | 1.181 | 965 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 100 | `WMYCR` / `WMYCR` | Criminal | 0,233 | 0,236 | 1.314 | 1.229 | 0,141 | 2 / 2 | Carcer City, Los Santos | — |
| 101 | `WMYST` / `WMYST` | Dân thường | 0,213 | 0,215 | 1.258 | 1.154 | 0,125 | 1 / 1 | Carcer City, Los Santos | P1 |
| 102 | `BALLAS1` / `BALLAS1` | Gang | 0,208 | 0,211 | 1.230 | 1.064 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 103 | `BALLAS2` / `BALLAS2` | Gang | 0,097 | 0,100 | 1.161 | 1.069 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 104 | `BALLAS3` / `BALLAS3` | Gang | 0,210 | 0,213 | 1.188 | 1.135 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 105 | `FAM1` / `FAM1` | Gang | 0,093 | 0,096 | 1.113 | 1.011 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 106 | `FAM2` / `FAM2` | Gang | 0,110 | 0,111 | 1.416 | 1.218 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 107 | `FAM3` / `FAM3` | Gang | 0,116 | 0,119 | 1.254 | 1.326 | 0,020 | 2 / 2 | Carcer City, Los Santos | — |
| 108 | `LSV1` / `LSV1` | Gang | 0,210 | 0,213 | 1.195 | 1.122 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 109 | `LSV2` / `LSV2` | Gang | 0,212 | 0,215 | 1.197 | 1.160 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 110 | `LSV3` / `LSV3` | Gang | 0,234 | 0,236 | 1.324 | 1.234 | 0,141 | 2 / 2 | Carcer City, Los Santos | — |
| 111 | `MAFFA` / `MAFFA` | Gang | 0,199 | 0,201 | 1.060 | 950 | 0,125 | 1 / 1 | Los Santos | — |
| 112 | `MAFFB` / `MAFFB` | Gang | 0,197 | 0,199 | 1.058 | 909 | 0,125 | 1 / 1 | Los Santos | — |
| 113 | `MAFBOSS` / `MAFBOSS` | Gang | 0,196 | 0,199 | 935 | 940 | 0,125 | 1 / 1 | Los Santos | — |
| 114 | `VLA1` / `VLA1` | Gang | 0,209 | 0,211 | 1.238 | 1.085 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 115 | `VLA2` / `VLA2` | Gang | 0,232 | 0,234 | 1.264 | 1.227 | 0,141 | 2 / 2 | Carcer City, Los Santos | — |
| 116 | `VLA3` / `VLA3` | Gang | 0,232 | 0,234 | 1.305 | 1.209 | 0,141 | 2 / 2 | Carcer City, Los Santos | — |
| 117 | `TRIADA` / `TRIADA` | Gang | 0,200 | 0,203 | 1.140 | 945 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 118 | `TRIADB` / `TRIADB` | Gang | 0,200 | 0,203 | 1.140 | 944 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 120 | `TRIBOSS` / `TRIBOSS` | Gang | 0,211 | 0,213 | 1.182 | 1.143 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 121 | `DNB1` / `DNB1` | Gang | 0,203 | 0,205 | 1.168 | 996 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 122 | `DNB2` / `DNB2` | Gang | 0,205 | 0,207 | 1.134 | 1.037 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 123 | `DNB3` / `DNB3` | Gang | 0,210 | 0,213 | 1.148 | 1.145 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 124 | `VMAFF1` / `VMAFF1` | Gang | 0,200 | 0,203 | 1.125 | 942 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 125 | `VMAFF2` / `VMAFF2` | Gang | 0,186 | 0,189 | 944 | 738 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 126 | `VMAFF3` / `VMAFF3` | Gang | 0,211 | 0,215 | 1.283 | 1.113 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 127 | `VMAFF4` / `VMAFF4` | Gang | 0,205 | 0,209 | 1.078 | 1.075 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 128 | `DNMYLC` / `DNMYLC` | Dân thường | 0,194 | 0,197 | 1.045 | 858 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 129 | `DNFOLC1` / `DNFOLC1` | Dân thường | 0,190 | 0,193 | 944 | 810 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 130 | `DNFOLC2` / `DNFOLC2` | Dân thường | 0,193 | 0,195 | 967 | 877 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 131 | `DNFYLC` / `DNFYLC` | Dân thường | 0,189 | 0,191 | 1.006 | 765 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 132 | `DNMOLC1` / `DNMOLC1` | Dân thường | 0,189 | 0,191 | 944 | 787 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 133 | `DNMOLC2` / `DNMOLC2` | Dân thường | 0,188 | 0,191 | 1.002 | 754 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 134 | `SBMOTR2` / `SBMOTR2` | Dân thường | 0,191 | 0,193 | 960 | 826 | 0,125 | 1 / 1 | Carcer City | — |
| 135 | `SWMOTR2` / `SWMOTR2` | Dân thường | 0,192 | 0,193 | 932 | 853 | 0,125 | 1 / 1 | Carcer City | — |
| 136 | `SBMYTR3` / `SBMYTR3` | Dân thường | 0,187 | 0,189 | 946 | 750 | 0,125 | 1 / 1 | Carcer City | — |
| 137 | `SWMOTR3` / `SWMOTR3` | Dân thường | 0,195 | 0,197 | 919 | 918 | 0,125 | 1 / 1 | Carcer City | — |
| 138 | `WFYBE` / `WFYBE` | Dân thường | 0,217 | 0,219 | 1.308 | 1.218 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 139 | `BFYBE` / `BFYBE` | Dân thường | 0,211 | 0,215 | 1.242 | 1.134 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 140 | `HFYBE` / `HFYBE` | Dân thường | 0,106 | 0,109 | 1.308 | 1.195 | 0,016 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 141 | `SOFYBU` / `SOFYBU` | Dân thường | 0,233 | 0,236 | 1.178 | 1.270 | 0,141 | 2 / 2 | Vice City, Carcer City, Los Santos | — |
| 142 | `SBMYST` / `SBMYST` | Dân thường | 0,199 | 0,201 | 1.046 | 953 | 0,125 | 1 / 1 | Carcer City | P1 |
| 143 | `SBMYCR` / `SBMYCR` | Criminal | 0,199 | 0,201 | 1.020 | 970 | 0,125 | 1 / 1 | Carcer City | — |
| 144 | `BMYCG` / `bmycg` | Criminal | 0,204 | 0,207 | 1.076 | 1.050 | 0,125 | 1 / 1 | — | — |
| 145 | `WFYCRK` / `Wfycrk` | Dân thường | 0,210 | 0,213 | 1.234 | 1.107 | 0,125 | 1 / 1 | — | — |
| 146 | `HMYCM` / `hmycm` | Criminal | 0,143 | 0,145 | 1.130 | 1.048 | 0,062 | 1 / 1 | — | — |
| 147 | `WMYBU` / `wmybu` | Dân thường | 0,184 | 0,188 | 844 | 735 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | P1 |
| 148 | `BFYBU` / `bfybu` | Dân thường | 0,209 | 0,211 | 1.052 | 1.159 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 150 | `WFYBU` / `wfybu` | Dân thường | 0,210 | 0,213 | 1.123 | 1.152 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | P1 |
| 151 | `DWFYLC1` / `Dwfylc1` | Dân thường | 0,192 | 0,195 | 1.007 | 825 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 152 | `WFYPRO` / `WFYpro` | Prostitute | 0,216 | 0,219 | 1.209 | 1.239 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 153 | `WMYCONB` / `wmyconb` | Dân thường | 0,191 | 0,193 | 908 | 855 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 154 | `WMYBE` / `wmybe` | Dân thường | 0,190 | 0,193 | 1.090 | 757 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 155 | `WMYPIZZ` / `wmypizz` | Dân thường | 0,205 | 0,207 | 1.102 | 1.061 | 0,125 | 1 / 1 | — | — |
| 156 | `BMOBAR` / `bmobar` | Dân thường | 0,213 | 0,215 | 1.028 | 919 | 0,141 | 2 / 2 | — | — |
| 157 | `CWFYHB` / `cwfyhb` | Dân thường | 0,194 | 0,197 | 1.046 | 859 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 158 | `CWMOFR` / `cwmofr` | Dân thường | 0,186 | 0,189 | 911 | 747 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 159 | `CWMOHB1` / `cwmohb1` | Dân thường | 0,187 | 0,189 | 1.003 | 727 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 160 | `CWMOHB2` / `cwmohb2` | Dân thường | 0,194 | 0,197 | 967 | 889 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 161 | `CWMYFR` / `cwmyfr` | Dân thường | 0,189 | 0,191 | 965 | 783 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 162 | `CWMYHB1` / `cwmyhb1` | Dân thường | 0,185 | 0,188 | 974 | 713 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 163 | `BMYBOUN` / `bmyboun` | Dân thường | 0,188 | 0,191 | 901 | 797 | 0,125 | 1 / 1 | — | — |
| 164 | `WMYBOUN` / `wmyboun` | Dân thường | 0,189 | 0,191 | 919 | 802 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 165 | `WMOMIB` / `wmomib` | Dân thường | 0,213 | 0,215 | 1.330 | 1.124 | 0,125 | 1 / 1 | — | — |
| 166 | `BMYMIB` / `bmymib` | Dân thường | 0,212 | 0,215 | 1.330 | 1.110 | 0,125 | 1 / 1 | — | — |
| 167 | `WMYBELL` / `wmybell` | Dân thường | 0,189 | 0,191 | 954 | 802 | 0,125 | 1 / 1 | — | — |
| 168 | `BMOCHIL` / `bmochil` | Dân thường | 0,192 | 0,195 | 1.001 | 833 | 0,125 | 1 / 1 | — | — |
| 169 | `SOFYRI` / `sofyri` | Dân thường | 0,222 | 0,225 | 1.190 | 1.359 | 0,125 | 1 / 1 | Carcer City | — |
| 170 | `SOMYST` / `somyst` | Dân thường | 0,204 | 0,207 | 1.106 | 1.037 | 0,125 | 1 / 1 | Carcer City | P1 |
| 171 | `VWMYBJD` / `vwmybjd` | Dân thường | 0,202 | 0,205 | 1.074 | 1.015 | 0,125 | 1 / 1 | — | — |
| 172 | `VWFYCRP` / `vwfycrp` | Dân thường | 0,207 | 0,209 | 1.129 | 1.090 | 0,125 | 1 / 1 | — | — |
| 173 | `SFR1` / `SFR1` | Gang | 0,221 | 0,225 | 1.335 | 1.296 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 174 | `SFR2` / `SFR2` | Gang | 0,233 | 0,236 | 1.300 | 1.231 | 0,141 | 2 / 2 | Carcer City, Los Santos | — |
| 175 | `SFR3` / `SFR3` | Gang | 0,218 | 0,221 | 1.290 | 1.239 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 176 | `BMYBAR` / `BMYBAR` | Dân thường | 0,201 | 0,203 | 1.052 | 995 | 0,125 | 1 / 1 | — | — |
| 177 | `WMYBAR` / `WMYBAR` | Dân thường | 0,202 | 0,205 | 1.070 | 1.012 | 0,125 | 1 / 1 | — | — |
| 178 | `WFYSEX` / `WFYSEX` | Dân thường | 0,217 | 0,219 | 1.240 | 1.242 | 0,125 | 1 / 1 | — | — |
| 179 | `WMYAMMO` / `WMYAMMO` | Dân thường | 0,211 | 0,213 | 1.250 | 1.119 | 0,125 | 1 / 1 | — | — |
| 180 | `BMYTATT` / `BMYTATT` | Dân thường | 0,204 | 0,207 | 1.074 | 1.056 | 0,125 | 1 / 1 | — | — |
| 181 | `VWMYCR` / `VWMYCR` | Criminal | 0,192 | 0,195 | 999 | 833 | 0,125 | 1 / 1 | Carcer City | — |
| 182 | `VBMOCD` / `VBMOCD` | Dân thường | 0,188 | 0,191 | 910 | 785 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 183 | `VBMYCR` / `VBMYCR` | Criminal | 0,187 | 0,189 | 916 | 759 | 0,125 | 1 / 1 | Carcer City | — |
| 184 | `VHMYCR` / `VHMYCR` | Criminal | 0,205 | 0,207 | 1.129 | 1.043 | 0,125 | 1 / 1 | Carcer City | — |
| 185 | `SBMYRI` / `SBMYRI` | Dân thường | 0,217 | 0,221 | 1.268 | 1.241 | 0,125 | 1 / 1 | Carcer City | P1 |
| 186 | `SOMYRI` / `SOMYRI` | Dân thường | 0,214 | 0,217 | 1.202 | 1.205 | 0,125 | 1 / 1 | Carcer City | P1 |
| 187 | `SOMYBU` / `SOMYBU` | Dân thường | 0,189 | 0,191 | 872 | 820 | 0,125 | 1 / 1 | Carcer City | — |
| 188 | `SWMYST` / `SWMYST` | Dân thường | 0,206 | 0,209 | 1.156 | 1.048 | 0,125 | 1 / 1 | Carcer City | P1 |
| 189 | `WMYVA` / `WMYVA` | Dân thường | 0,203 | 0,205 | 1.074 | 1.020 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 190 | `COPGRL3` / `COPGRL3` | Dân thường | 0,217 | 0,219 | 1.297 | 1.222 | 0,125 | 1 / 1 | — | — |
| 191 | `GUNGRL3` / `GUNGRL3` | Dân thường | 0,205 | 0,207 | 1.179 | 1.027 | 0,125 | 1 / 1 | — | — |
| 192 | `MECGRL3` / `MECGRL3` | Dân thường | 0,217 | 0,221 | 1.377 | 1.201 | 0,125 | 1 / 1 | — | — |
| 193 | `NURGRL3` / `NURGRL3` | Dân thường | 0,220 | 0,223 | 1.242 | 1.298 | 0,125 | 1 / 1 | — | — |
| 194 | `CROGRL3` / `CROGRL3` | Dân thường | 0,209 | 0,211 | 1.136 | 1.123 | 0,125 | 1 / 1 | — | — |
| 195 | `GANGRL3` / `GANGRL3` | Dân thường | 0,211 | 0,213 | 1.216 | 1.130 | 0,125 | 1 / 1 | — | — |
| 196 | `CWFOFR` / `CWFOFR` | Dân thường | 0,185 | 0,188 | 912 | 720 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 197 | `CWFOHB` / `CWFOHB` | Dân thường | 0,184 | 0,188 | 920 | 708 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 198 | `CWFYFR1` / `CWFYFR1` | Dân thường | 0,191 | 0,193 | 1.017 | 804 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 199 | `CWFYFR2` / `CWFYFR2` | Dân thường | 0,192 | 0,195 | 992 | 841 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 200 | `CWMYHB2` / `CWMYHB2` | Dân thường | 0,191 | 0,193 | 999 | 820 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 201 | `DWFYLC2` / `DWFYLC2` | Dân thường | 0,190 | 0,193 | 996 | 790 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 202 | `DWMYLC2` / `DWMYLC2` | Dân thường | 0,187 | 0,189 | 986 | 744 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 203 | `OMYKARA` / `OMYKARA` | Dân thường | 0,217 | 0,221 | 1.260 | 1.243 | 0,125 | 1 / 1 | — | — |
| 204 | `WMYKARA` / `WMYKARA` | Dân thường | 0,216 | 0,219 | 1.228 | 1.233 | 0,125 | 1 / 1 | — | — |
| 205 | `WFYBURG` / `WFYBURG` | Dân thường | 0,195 | 0,197 | 1.044 | 871 | 0,125 | 1 / 1 | — | — |
| 206 | `VWMYCD` / `VWMYCD` | Dân thường | 0,185 | 0,188 | 956 | 702 | 0,125 | 1 / 1 | Carcer City | — |
| 207 | `VHFYPRO` / `VHFYPRO` | Prostitute | 0,205 | 0,207 | 1.196 | 1.017 | 0,125 | 1 / 1 | Carcer City | — |
| 209 | `OMONOOD` / `OMONOOD` | Dân thường | 0,190 | 0,191 | 948 | 806 | 0,125 | 1 / 1 | — | — |
| 210 | `OMOBOAT` / `OMOBOAT` | Dân thường | 0,194 | 0,197 | 1.014 | 863 | 0,125 | 1 / 1 | — | — |
| 211 | `WFYCLOT` / `WFYCLOT` | Dân thường | 0,208 | 0,211 | 1.079 | 1.123 | 0,125 | 1 / 1 | — | — |
| 212 | `VWMOTR1` / `VWMOTR1` | Dân thường | 0,187 | 0,189 | 949 | 761 | 0,125 | 1 / 1 | Carcer City | — |
| 213 | `VWMOTR2` / `VWMOTR2` | Dân thường | 0,185 | 0,188 | 895 | 745 | 0,125 | 1 / 1 | Carcer City | — |
| 214 | `VWFYWAI` / `VWFYWAI` | Dân thường | 0,213 | 0,215 | 1.122 | 1.207 | 0,125 | 1 / 1 | — | — |
| 215 | `SBFORI` / `SBFORI` | Dân thường | 0,206 | 0,209 | 1.219 | 1.044 | 0,125 | 1 / 1 | Carcer City | — |
| 216 | `SWFYRI` / `SWFYRI` | Dân thường | 0,213 | 0,217 | 1.124 | 1.220 | 0,125 | 1 / 1 | Carcer City | P1 |
| 217 | `WMYCLOT` / `WMYCLOT` | Dân thường | 0,210 | 0,213 | 1.208 | 1.109 | 0,125 | 1 / 1 | — | — |
| 218 | `SBFOST` / `SBFOST` | Dân thường | 0,187 | 0,189 | 1.024 | 725 | 0,125 | 1 / 1 | Carcer City | — |
| 219 | `SBFYRI` / `SBFYRI` | Dân thường | 0,220 | 0,223 | 1.209 | 1.323 | 0,125 | 1 / 1 | Carcer City | P1 |
| 220 | `SBMOCD` / `SBMOCD` | Dân thường | 0,191 | 0,193 | 946 | 846 | 0,125 | 1 / 1 | Los Santos | — |
| 221 | `SBMORI` / `SBMORI` | Dân thường | 0,198 | 0,201 | 1.022 | 957 | 0,125 | 1 / 1 | Carcer City | — |
| 222 | `SBMOST` / `SBMOST` | Dân thường | 0,198 | 0,201 | 1.020 | 955 | 0,125 | 1 / 1 | Carcer City | — |
| 223 | `SHMYCR` / `SHMYCR` | Criminal | 0,245 | 0,248 | 1.224 | 1.189 | 0,156 | 2 / 2 | Carcer City | — |
| 224 | `SOFORI` / `SOFORI` | Dân thường | 0,210 | 0,213 | 1.199 | 1.122 | 0,125 | 1 / 1 | Carcer City | — |
| 225 | `SOFOST` / `SOFOST` | Dân thường | 0,203 | 0,205 | 1.195 | 979 | 0,125 | 1 / 1 | Carcer City | — |
| 226 | `SOFYST` / `SOFYST` | Dân thường | 0,205 | 0,207 | 1.056 | 1.069 | 0,125 | 1 / 1 | Carcer City | P1 |
| 227 | `SOMOBU` / `SOMOBU` | Dân thường | 0,188 | 0,189 | 964 | 762 | 0,125 | 1 / 1 | Carcer City | — |
| 228 | `SOMORI` / `SOMORI` | Dân thường | 0,208 | 0,211 | 1.094 | 1.132 | 0,125 | 1 / 1 | Carcer City | — |
| 229 | `SOMOST` / `SOMOST` | Dân thường | 0,192 | 0,195 | 1.019 | 825 | 0,125 | 1 / 1 | Carcer City | P1 |
| 230 | `SWMOTR5` / `SWMOTR5` | Dân thường | 0,189 | 0,191 | 935 | 806 | 0,125 | 1 / 1 | Carcer City | — |
| 231 | `SWFORI` / `SWFORI` | Dân thường | 0,193 | 0,195 | 1.098 | 822 | 0,125 | 1 / 1 | Carcer City | — |
| 232 | `SWFOST` / `SWFOST` | Dân thường | 0,189 | 0,191 | 1.054 | 760 | 0,125 | 1 / 1 | Carcer City | — |
| 233 | `SWFYST` / `SWFYST` | Dân thường | 0,223 | 0,227 | 1.087 | 1.107 | 0,141 | 2 / 2 | Carcer City | P1 |
| 234 | `SWMOCD` / `SWMOCD` | Dân thường | 0,193 | 0,195 | 1.047 | 840 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 235 | `SWMORI` / `SWMORI` | Dân thường | 0,188 | 0,191 | 1.032 | 750 | 0,125 | 1 / 1 | Carcer City | — |
| 236 | `SWMOST` / `SWMOST` | Dân thường | 0,196 | 0,199 | 1.036 | 910 | 0,125 | 1 / 1 | Carcer City | — |
| 237 | `SHFYPRO` / `SHFYPRO` | Prostitute | 0,215 | 0,219 | 1.179 | 1.232 | 0,125 | 1 / 1 | Carcer City | — |
| 238 | `SBFYPRO` / `SBFYPRO` | Prostitute | 0,188 | 0,191 | 1.028 | 739 | 0,125 | 1 / 1 | Carcer City | — |
| 239 | `SWMOTR4` / `SWMOTR4` | Dân thường | 0,192 | 0,195 | 957 | 854 | 0,125 | 1 / 1 | Carcer City | — |
| 240 | `SWMYRI` / `SWMYRI` | Dân thường | 0,217 | 0,219 | 1.260 | 1.238 | 0,125 | 1 / 1 | Carcer City | P1 |
| 241 | `SMYST` / `SMYST` | Dân thường | 0,191 | 0,193 | 968 | 819 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 242 | `SMYST2` / `SMYST2` | Dân thường | 0,193 | 0,195 | 1.019 | 841 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 243 | `SFYPRO` / `SFYPRO` | Prostitute | 0,094 | 0,096 | 1.196 | 987 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 244 | `VBFYST2` / `VBFYST2` | Dân thường | 0,242 | 0,246 | 1.852 | 1.524 | 0,125 | 1 / 1 | — | — |
| 245 | `VBFYPRO` / `VBFYPRO` | Prostitute | 0,190 | 0,193 | 1.011 | 784 | 0,125 | 1 / 1 | Carcer City | — |
| 246 | `VHFYST3` / `VHFYST3` | Dân thường | 0,252 | 0,256 | 1.927 | 1.692 | 0,125 | 1 / 1 | — | — |
| 247 | `BIKERA` / `BIKERA` | Gang | 0,211 | 0,215 | 1.274 | 1.118 | 0,125 | 1 / 1 | Los Santos | — |
| 248 | `BIKERB` / `BIKERB` | Gang | 0,210 | 0,213 | 1.200 | 1.118 | 0,125 | 1 / 1 | Los Santos | — |
| 249 | `BMYPIMP` / `BMYPIMP` | Dân thường | 0,205 | 0,207 | 1.070 | 1.053 | 0,126 | 2 / 2 | — | — |
| 250 | `SWMYCR` / `SWMYCR` | Criminal | 0,206 | 0,209 | 1.129 | 1.076 | 0,125 | 1 / 1 | Carcer City | — |
| 251 | `WFYLG` / `WFYLG` | Dân thường | 0,212 | 0,215 | 1.270 | 1.126 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 252 | `WMYVA2` / `WMYVA2` | Dân thường | 0,190 | 0,193 | 1.070 | 768 | 0,125 | 1 / 1 | — | — |
| 253 | `BMOSEC` / `BMOSEC` | Dân thường | 0,187 | 0,189 | 901 | 775 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 254 | `BIKDRUG` / `BIKDRUG` | Dân thường | 0,211 | 0,215 | 1.274 | 1.118 | 0,125 | 1 / 1 | Vice City, Carcer City, Los Santos | — |
| 255 | `WMYCH` / `WMYCH` | Dân thường | 0,192 | 0,195 | 942 | 855 | 0,125 | 1 / 1 | Los Santos | — |
| 256 | `SBFYSTR` / `SBFYSTR` | Dân thường | 0,253 | 0,256 | 2.048 | 1.664 | 0,125 | 1 / 1 | — | — |
| 257 | `SWFYSTR` / `SWFYSTR` | Dân thường | 0,252 | 0,256 | 1.985 | 1.671 | 0,125 | 1 / 1 | — | — |
| 258 | `HECK1` / `HECK1` | Dân thường | 0,201 | 0,203 | 1.160 | 947 | 0,125 | 1 / 1 | — | — |
| 259 | `HECK2` / `HECK2` | Dân thường | 0,219 | 0,223 | 1.438 | 1.213 | 0,125 | 1 / 1 | — | — |
| 260 | `BMYCON` / `BMYCON` | Dân thường | 0,213 | 0,215 | 1.242 | 1.167 | 0,125 | 1 / 1 | — | — |
| 261 | `WMYCD1` / `WMYCD1` | Dân thường | 0,190 | 0,193 | 954 | 819 | 0,125 | 1 / 1 | Los Santos | — |
| 262 | `BMOCD` / `BMOCD` | Dân thường | 0,186 | 0,189 | 908 | 757 | 0,125 | 1 / 1 | Los Santos | — |
| 263 | `VWFYWA2` / `VWFYWA2` | Dân thường | 0,213 | 0,217 | 1.172 | 1.200 | 0,125 | 1 / 1 | — | — |
| 264 | `WMOICE` / `WMOICE` | Dân thường | 0,192 | 0,195 | 1.023 | 831 | 0,125 | 1 / 1 | — | — |
| 274 | `laemt1` / `laemt1` | Cảnh sát / quân đội / cứu hộ | 0,194 | 0,197 | 1.024 | 867 | 0,125 | 1 / 1 | Los Santos | — |
| 275 | `lvemt1` / `lvemt1` | Cảnh sát / quân đội / cứu hộ | 0,194 | 0,197 | 1.024 | 865 | 0,125 | 1 / 1 | — | — |
| 276 | `sfemt1` / `sfemt1` | Cảnh sát / quân đội / cứu hộ | 0,194 | 0,197 | 1.024 | 865 | 0,125 | 1 / 1 | — | — |
| 277 | `lafd1` / `lafd1` | Cảnh sát / quân đội / cứu hộ | 0,202 | 0,205 | 1.049 | 1.014 | 0,125 | 1 / 1 | Los Santos | — |
| 278 | `lvfd1` / `lvfd1` | Cảnh sát / quân đội / cứu hộ | 0,202 | 0,205 | 1.049 | 1.028 | 0,125 | 1 / 1 | — | — |
| 279 | `sffd1` / `sffd1` | Cảnh sát / quân đội / cứu hộ | 0,202 | 0,205 | 1.049 | 1.014 | 0,125 | 1 / 1 | — | — |
| 280 | `lapd1` / `lapd1` | Cảnh sát / quân đội / cứu hộ | 0,130 | 0,133 | 1.601 | 1.553 | 0,016 | 2 / 2 | Los Santos | NPC pilot đã thay |
| 281 | `sfpd1` / `sfpd1` | Cảnh sát / quân đội / cứu hộ | 0,198 | 0,201 | 1.066 | 922 | 0,125 | 1 / 1 | — | — |
| 282 | `lvpd1` / `lvpd1` | Cảnh sát / quân đội / cứu hộ | 0,198 | 0,201 | 1.046 | 930 | 0,125 | 1 / 1 | — | — |
| 283 | `csher` / `csher` | Cảnh sát / quân đội / cứu hộ | 0,098 | 0,102 | 1.218 | 1.068 | 0,016 | 1 / 1 | — | — |
| 284 | `lapdm1` / `lapdm1` | Cảnh sát / quân đội / cứu hộ | 0,090 | 0,094 | 1.010 | 982 | 0,016 | 1 / 1 | Los Santos | — |
| 285 | `swat` / `swat` | Cảnh sát / quân đội / cứu hộ | 0,356 | 0,357 | 3.622 | 3.113 | 0,125 | 1 / 4 | Los Santos | NPC pilot đã thay |
| 286 | `fbi` / `fbi` | Cảnh sát / quân đội / cứu hộ | 0,190 | 0,193 | 978 | 799 | 0,125 | 1 / 1 | Los Santos | — |
| 287 | `army` / `army` | Cảnh sát / quân đội / cứu hộ | 0,360 | 0,363 | 3.696 | 3.154 | 0,125 | 1 / 9 | Los Santos | NPC pilot đã thay |
| 288 | `dsher` / `dsher` | Cảnh sát / quân đội / cứu hộ | 0,208 | 0,211 | 1.218 | 1.067 | 0,125 | 1 / 1 | — | — |
| 290 | `special01` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 291 | `special02` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 292 | `special03` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 293 | `special04` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 294 | `special05` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 295 | `special06` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 296 | `special07` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 297 | `special08` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 298 | `special09` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 299 | `special10` / `generic` | Placeholder / slot động | — | — | — | — | — | — | — | Không yêu cầu cặp tĩnh |
| 48012 | `VCS_ALBERTO` / `VCS_ALBERTO` | Dân thường | 0,114 | 0,115 | 1.050 | 1.554 | 0,009 | 7 / 7 | — | — |
| 48013 | `VCS_ARMANDO` / `VCS_ARMANDO` | Dân thường | 0,150 | 0,150 | 1.014 | 1.538 | 0,046 | 7 / 7 | — | — |
| 48014 | `VCS_ARMY` / `VCS_ARMY` | Cảnh sát / quân đội / cứu hộ | 0,112 | 0,113 | 1.056 | 1.553 | 0,006 | 6 / 6 | Vice City | Đuôi nonzero DFF,TXD |
| 48015 | `VCS_BCOP` / `VCS_BCOP` | Cảnh sát / quân đội / cứu hộ | 0,116 | 0,117 | 996 | 1.520 | 0,012 | 8 / 8 | Vice City | — |
| 48016 | `VCS_BFOBE` / `VCS_BFOBE` | Dân thường | 0,109 | 0,111 | 994 | 1.464 | 0,010 | 6 / 6 | Vice City | — |
| 48017 | `VCS_BFORI` / `VCS_BFORI` | Dân thường | 0,110 | 0,111 | 1.028 | 1.529 | 0,007 | 7 / 7 | Vice City | — |
| 48018 | `VCS_BFOST` / `VCS_BFOST` | Dân thường | 0,107 | 0,109 | 1.018 | 1.457 | 0,008 | 5 / 6 | — | — |
| 48019 | `VCS_BFOTR` / `VCS_BFOTR` | Dân thường | 0,105 | 0,107 | 952 | 1.432 | 0,008 | 5 / 5 | — | — |
| 48020 | `VCS_BFYBE` / `VCS_BFYBE` | Dân thường | 0,112 | 0,115 | 1.036 | 1.554 | 0,007 | 6 / 6 | Vice City | — |
| 48021 | `VCS_BFYPR` / `VCS_BFYPR` | Prostitute | 0,109 | 0,109 | 994 | 1.437 | 0,010 | 6 / 6 | Vice City | — |
| 48022 | `VCS_BFYRI` / `VCS_BFYRI` | Dân thường | 0,108 | 0,111 | 990 | 1.482 | 0,007 | 8 / 8 | Vice City | P1 |
| 48023 | `VCS_BFYST` / `VCS_BFYST` | Dân thường | 0,112 | 0,115 | 1.036 | 1.551 | 0,007 | 7 / 7 | Vice City | — |
| 48024 | `VCS_BMOBE` / `VCS_BMOBE` | Dân thường | 0,112 | 0,113 | 1.058 | 1.516 | 0,009 | 6 / 7 | — | — |
| 48025 | `VCS_BMODK` / `VCS_BMODK` | Dân thường | 0,114 | 0,117 | 1.008 | 1.558 | 0,009 | 7 / 8 | Vice City | — |
| 48026 | `VCS_BMOST` / `VCS_BMOST` | Dân thường | 0,117 | 0,119 | 1.092 | 1.631 | 0,007 | 7 / 7 | — | — |
| 48027 | `VCS_BMOTR` / `VCS_BMOTR` | Dân thường | 0,112 | 0,113 | 984 | 1.495 | 0,011 | 7 / 8 | Vice City | — |
| 48028 | `VCS_BMYBB` / `VCS_BMYBB` | Dân thường | 0,106 | 0,109 | 972 | 1.451 | 0,008 | 6 / 7 | — | — |
| 48029 | `VCS_BMYBE` / `VCS_BMYBE` | Dân thường | 0,108 | 0,111 | 1.000 | 1.484 | 0,008 | 5 / 6 | — | — |
| 48030 | `VCS_BMYBU` / `VCS_BMYBU` | Dân thường | 0,110 | 0,111 | 955 | 1.405 | 0,014 | 5 / 7 | Vice City | — |
| 48031 | `VCS_BMYCR` / `VCS_BMYCR` | Criminal | 0,099 | 0,102 | 928 | 1.372 | 0,006 | 6 / 7 | Vice City | — |
| 48032 | `VCS_BMYPI` / `VCS_BMYPI` | Dân thường | 0,119 | 0,121 | 1.080 | 1.603 | 0,010 | 8 / 9 | Vice City | P1 |
| 48033 | `VCS_BMYRI` / `VCS_BMYRI` | Dân thường | 0,108 | 0,109 | 1.001 | 1.500 | 0,007 | 6 / 7 | Vice City | P1 |
| 48034 | `VCS_BMYST` / `VCS_BMYST` | Dân thường | 0,101 | 0,104 | 946 | 1.376 | 0,006 | 6 / 8 | Vice City | P1 |
| 48035 | `VCS_BURGER` / `VCS_BURGER` | Dân thường | 0,112 | 0,115 | 1.024 | 1.495 | 0,009 | 8 / 10 | — | — |
| 48036 | `VCS_COKHED` / `VCS_COKHED` | Gang | 0,114 | 0,115 | 1.004 | 1.500 | 0,012 | 8 / 8 | — | — |
| 48037 | `VCS_COP` / `VCS_COP` | Cảnh sát / quân đội / cứu hộ | 0,104 | 0,105 | 954 | 1.399 | 0,009 | 7 / 7 | Vice City | — |
| 48038 | `VCS_CS_DASS1` / `VCS_CS_DASS1` | Gang | 0,299 | 0,301 | 1.996 | 3.031 | 0,102 | 8 / 8 | — | Đuôi nonzero DFF |
| 48039 | `VCS_CS_DASS2` / `VCS_CS_DASS2` | Gang | 0,289 | 0,291 | 1.882 | 2.877 | 0,102 | 8 / 8 | — | Đuôi nonzero DFF |
| 48040 | `VCS_CS_DIAZ` / `VCS_CS_DIAZ` | Gang | 0,243 | 0,244 | 1.944 | 2.965 | 0,049 | 10 / 10 | — | — |
| 48041 | `VCS_CS_FORBES` / `VCS_CS_FORBES` | Gang | 4,404 | 4,406 | 2.004 | 3.098 | 4,203 | 9 / 9 | — | Đuôi nonzero DFF |
| 48042 | `VCS_CS_JANET` / `VCS_CS_JANET` | Gang | 0,230 | 0,232 | 1.922 | 2.778 | 0,047 | 8 / 8 | — | — |
| 48043 | `VCS_CS_LOUISE3` / `VCS_CS_LOUISE3` | Gang | 4,540 | 4,541 | 1.954 | 3.019 | 4,344 | 9 / 9 | — | Đuôi nonzero DFF |
| 48044 | `VCS_CS_MAN1` / `VCS_CS_MAN1` | Gang | 2,838 | 2,840 | 1.805 | 2.500 | 2,672 | 6 / 6 | — | Đuôi nonzero DFF |
| 48045 | `VCS_CS_MARYJ` / `VCS_CS_MARYJ` | Gang | 0,227 | 0,230 | 1.930 | 2.774 | 0,044 | 7 / 7 | — | — |
| 48046 | `VCS_CS_PED1` / `VCS_CS_PED1` | Gang | 4,825 | 4,828 | 1.926 | 2.812 | 4,641 | 8 / 8 | — | Đuôi nonzero DFF |
| 48047 | `VCS_CS_PHCOLLINS2` / `VCS_CS_PHCOLLINS2` | Gang | 3,449 | 3,451 | 2.020 | 3.062 | 3,250 | 8 / 8 | — | Đuôi nonzero DFF |
| 48048 | `VCS_CS_RENOP` / `VCS_CS_RENOP` | Gang | 5,107 | 5,109 | 2.038 | 3.080 | 4,906 | 10 / 10 | — | Đuôi nonzero DFF |
| 48049 | `VCS_CS_TROY` / `VCS_CS_TROY` | Gang | 3,879 | 3,881 | 1.970 | 2.924 | 3,688 | 10 / 10 | — | Đuôi nonzero DFF |
| 48050 | `VCS_CWMYHB2` / `VCS_CWMYHB2` | Gang | 0,136 | 0,139 | 1.154 | 1.660 | 0,023 | 8 / 8 | — | — |
| 48051 | `VCS_DEA1` / `VCS_DEA1` | Cảnh sát / quân đội / cứu hộ | 0,109 | 0,111 | 944 | 1.416 | 0,011 | 9 / 10 | — | — |
| 48052 | `VCS_DEA2` / `VCS_DEA2` | Cảnh sát / quân đội / cứu hộ | 0,110 | 0,113 | 942 | 1.410 | 0,013 | 9 / 9 | — | — |
| 48053 | `VCS_DIAZ` / `VCS_DIAZ` | Dân thường | 0,242 | 0,244 | 1.944 | 2.965 | 0,048 | 10 / 10 | — | — |
| 48054 | `VCS_DIEGO` / `VCS_DIEGO` | Dân thường | 0,144 | 0,146 | 1.088 | 1.594 | 0,035 | 9 / 9 | — | — |
| 48055 | `VCS_FBI` / `VCS_FBI` | Cảnh sát / quân đội / cứu hộ | 0,109 | 0,111 | 995 | 1.464 | 0,008 | 10 / 10 | Vice City | — |
| 48056 | `VCS_FILMCRW` / `VCS_FILMCRW` | Gang | 0,078 | 0,080 | 1.012 | 768 | 0,012 | 9 / 9 | — | — |
| 48057 | `VCS_FIREMEN` / `VCS_FIREMEN` | Cảnh sát / quân đội / cứu hộ | 0,107 | 0,109 | 964 | 1.407 | 0,010 | 8 / 8 | — | — |
| 48058 | `VCS_GANG1A` / `VCS_GANG1A` | Gang | 0,108 | 0,109 | 976 | 1.401 | 0,011 | 8 / 8 | Vice City | — |
| 48059 | `VCS_GANG1B` / `VCS_GANG1B` | Gang | 0,131 | 0,133 | 988 | 1.442 | 0,032 | 7 / 7 | Vice City | — |
| 48060 | `VCS_GANG1C` / `VCS_GANG1C` | Gang | 0,205 | 0,209 | 1.796 | 2.692 | 0,029 | 7 / 7 | — | Đuôi nonzero DFF |
| 48061 | `VCS_GANG1D` / `VCS_GANG1D` | Gang | 0,220 | 0,223 | 1.920 | 2.885 | 0,031 | 8 / 8 | — | Đuôi nonzero DFF |
| 48062 | `VCS_GANG2A` / `VCS_GANG2A` | Gang | 0,105 | 0,107 | 970 | 1.376 | 0,010 | 8 / 8 | Vice City | — |
| 48063 | `VCS_GANG2B` / `VCS_GANG2B` | Gang | 0,105 | 0,107 | 960 | 1.382 | 0,010 | 8 / 8 | Vice City | — |
| 48064 | `VCS_GANG3A` / `VCS_GANG3A` | Gang | 0,105 | 0,107 | 951 | 1.408 | 0,009 | 8 / 8 | Vice City | — |
| 48065 | `VCS_GANG3B` / `VCS_GANG3B` | Gang | 0,107 | 0,109 | 968 | 1.454 | 0,008 | 7 / 8 | Vice City | — |
| 48066 | `VCS_GANG4A` / `VCS_GANG4A` | Cảnh sát / quân đội / cứu hộ | 0,101 | 0,104 | 879 | 1.296 | 0,011 | 8 / 8 | Vice City | — |
| 48067 | `VCS_GANG4B` / `VCS_GANG4B` | Cảnh sát / quân đội / cứu hộ | 0,101 | 0,104 | 896 | 1.306 | 0,011 | 7 / 7 | Vice City | — |
| 48068 | `VCS_GANG5A` / `VCS_GANG5A` | Cảnh sát / quân đội / cứu hộ | 0,112 | 0,113 | 961 | 1.463 | 0,012 | 9 / 9 | — | — |
| 48069 | `VCS_GANG5B` / `VCS_GANG5B` | Cảnh sát / quân đội / cứu hộ | 0,111 | 0,113 | 933 | 1.377 | 0,015 | 9 / 9 | — | — |
| 48070 | `VCS_GANG6A` / `VCS_GANG6A` | Gang | 0,113 | 0,115 | 1.058 | 1.540 | 0,008 | 9 / 9 | Vice City | — |
| 48071 | `VCS_GANG6B` / `VCS_GANG6B` | Gang | 0,105 | 0,107 | 972 | 1.402 | 0,008 | 9 / 9 | Vice City | — |
| 48072 | `VCS_GANG7A` / `VCS_GANG7A` | Gang | 0,109 | 0,111 | 1.018 | 1.475 | 0,008 | 8 / 8 | Vice City | — |
| 48073 | `VCS_GANG7B` / `VCS_GANG7B` | Gang | 0,112 | 0,113 | 1.016 | 1.523 | 0,008 | 8 / 9 | Vice City | — |
| 48074 | `VCS_GANG8A` / `VCS_GANG8A` | Dân thường | 0,100 | 0,102 | 907 | 1.290 | 0,010 | 8 / 8 | Vice City | — |
| 48075 | `VCS_GANG8B` / `VCS_GANG8B` | Dân thường | 0,116 | 0,119 | 1.046 | 1.530 | 0,011 | 9 / 9 | Vice City | — |
| 48076 | `VCS_LOW_EMPA` / `VCS_LOW_EMPA` | Gang | 0,110 | 0,111 | 998 | 1.460 | 0,010 | 8 / 9 | Vice City | — |
| 48077 | `VCS_LOW_EMPB` / `VCS_LOW_EMPB` | Gang | 0,108 | 0,111 | 988 | 1.451 | 0,009 | 7 / 7 | Vice City | — |
| 48078 | `VCS_GON_GOONA` / `VCS_GON_GOONA` | Gang | 0,072 | 0,072 | 971 | 700 | 0,010 | 7 / 7 | — | — |
| 48079 | `VCS_GON_GOONB` / `VCS_GON_GOONB` | Gang | 0,074 | 0,076 | 995 | 742 | 0,010 | 7 / 7 | — | — |
| 48080 | `VCS_GTR1` / `VCS_GTR1` | Dân thường | 0,123 | 0,125 | 1.092 | 1.670 | 0,011 | 8 / 8 | — | — |
| 48081 | `VCS_GTR2` / `VCS_GTR2` | Dân thường | 0,133 | 0,135 | 1.156 | 1.754 | 0,015 | 9 / 9 | — | — |
| 48082 | `VCS_HFOBE` / `VCS_HFOBE` | Dân thường | 0,108 | 0,111 | 990 | 1.402 | 0,012 | 6 / 7 | — | — |
| 48083 | `VCS_HFORI` / `VCS_HFORI` | Dân thường | 0,109 | 0,109 | 1.022 | 1.498 | 0,007 | 7 / 7 | Vice City | — |
| 48084 | `VCS_HFOST` / `VCS_HFOST` | Dân thường | 0,113 | 0,115 | 1.088 | 1.548 | 0,007 | 6 / 7 | — | — |
| 48085 | `VCS_HFOTR` / `VCS_HFOTR` | Dân thường | 0,111 | 0,113 | 1.004 | 1.497 | 0,010 | 6 / 7 | Vice City | — |
| 48086 | `VCS_HFYBE` / `VCS_HFYBE` | Dân thường | 0,108 | 0,111 | 1.030 | 1.466 | 0,007 | 6 / 9 | — | — |
| 48087 | `VCS_HFYBU` / `VCS_HFYBU` | Dân thường | 0,104 | 0,105 | 980 | 1.397 | 0,008 | 7 / 7 | Vice City | P1 |
| 48088 | `VCS_HFYCG` / `VCS_HFYCG` | Dân thường | 0,120 | 0,121 | 1.064 | 1.604 | 0,012 | 6 / 8 | — | — |
| 48089 | `VCS_HFYMD` / `VCS_HFYMD` | Dân thường | 0,114 | 0,117 | 1.032 | 1.520 | 0,011 | 5 / 6 | — | — |
| 48090 | `VCS_HFYPR` / `VCS_HFYPR` | Prostitute | 0,110 | 0,111 | 1.030 | 1.504 | 0,008 | 5 / 5 | Vice City | — |
| 48091 | `VCS_HFYRI` / `VCS_HFYRI` | Dân thường | 0,107 | 0,107 | 1.010 | 1.471 | 0,006 | 7 / 7 | Vice City | P1 |
| 48092 | `VCS_HFYST` / `VCS_HFYST` | Dân thường | 0,108 | 0,109 | 1.016 | 1.487 | 0,006 | 6 / 7 | Vice City | — |
| 48093 | `VCS_HIGH_EMPA` / `VCS_HIGH_EMPA` | Gang | 0,071 | 0,072 | 977 | 718 | 0,009 | 6 / 6 | Vice City | — |
| 48094 | `VCS_HIGH_EMPB` / `VCS_HIGH_EMPB` | Gang | 0,100 | 0,102 | 907 | 1.310 | 0,010 | 6 / 6 | Vice City | Tên texture cần xác minh: gang9b_trousers |
| 48095 | `VCS_HITMAN` / `VCS_HITMAN` | Cảnh sát / quân đội / cứu hộ | 0,111 | 0,113 | 1.004 | 1.482 | 0,010 | 6 / 6 | — | Đuôi nonzero TXD |
| 48096 | `VCS_HMOBE` / `VCS_HMOBE` | Dân thường | 0,116 | 0,119 | 1.057 | 1.546 | 0,011 | 6 / 6 | Vice City | — |
| 48097 | `VCS_HMOCA` / `VCS_HMOCA` | Dân thường | 0,098 | 0,100 | 889 | 1.281 | 0,010 | 7 / 7 | Vice City | — |
| 48098 | `VCS_HMORI` / `VCS_HMORI` | Dân thường | 0,102 | 0,104 | 961 | 1.392 | 0,007 | 5 / 8 | Vice City | — |
| 48099 | `VCS_HMOST` / `VCS_HMOST` | Dân thường | 0,097 | 0,100 | 901 | 1.320 | 0,007 | 6 / 6 | Vice City | P1 |
| 48100 | `VCS_HMOTR` / `VCS_HMOTR` | Dân thường | 0,103 | 0,105 | 940 | 1.409 | 0,008 | 5 / 6 | Vice City | — |
| 48101 | `VCS_HMYAP` / `VCS_HMYAP` | Dân thường | 0,099 | 0,102 | 921 | 1.329 | 0,007 | 7 / 7 | — | — |
| 48102 | `VCS_HMYBE` / `VCS_HMYBE` | Dân thường | 0,109 | 0,111 | 1.044 | 1.492 | 0,007 | 6 / 6 | — | — |
| 48103 | `VCS_HMYRI` / `VCS_HMYRI` | Dân thường | 0,103 | 0,105 | 967 | 1.419 | 0,007 | 6 / 6 | Vice City | P1 |
| 48104 | `VCS_HMYST` / `VCS_HMYST` | Dân thường | 0,107 | 0,109 | 990 | 1.435 | 0,008 | 9 / 9 | Vice City | P1 |
| 48105 | `VCS_JERRY` / `VCS_JERRY` | Gang | 0,155 | 0,158 | 1.188 | 1.682 | 0,040 | 8 / 8 | — | — |
| 48106 | `VCS_JFOTO` / `VCS_JFOTO` | Dân thường | 0,110 | 0,111 | 970 | 1.440 | 0,012 | 8 / 8 | — | — |
| 48107 | `VCS_JMOTO` / `VCS_JMOTO` | Dân thường | 0,105 | 0,105 | 965 | 1.368 | 0,010 | 8 / 8 | — | — |
| 48108 | `VCS_MALE01` / `VCS_MALE01` | Dân thường | 0,099 | 0,102 | 907 | 1.306 | 0,009 | 6 / 7 | — | — |
| 48109 | `VCS_MEDIC` / `VCS_MEDIC` | Cảnh sát / quân đội / cứu hộ | 0,100 | 0,104 | 905 | 1.320 | 0,009 | 7 / 7 | Vice City | — |
| 48110 | `VCS_MENDEZ1` / `VCS_MENDEZ1` | Gang | 4,887 | 4,889 | 1.936 | 2.781 | 4,703 | 9 / 9 | — | Đuôi nonzero DFF |
| 48111 | `VCS_MENDEZ2` / `VCS_MENDEZ2` | Gang | 4,897 | 4,898 | 2.034 | 2.950 | 4,703 | 9 / 9 | — | Đuôi nonzero DFF |
| 48112 | `VCS_MENGGA` / `VCS_MENGGA` | Gang | 0,144 | 0,145 | 986 | 1.513 | 0,041 | 8 / 8 | — | — |
| 48113 | `VCS_MENGGB` / `VCS_MENGGB` | Gang | 0,144 | 0,145 | 986 | 1.513 | 0,041 | 8 / 8 | — | — |
| 48114 | `VCS_PHIL` / `VCS_PHIL` | Gang | 0,154 | 0,156 | 1.278 | 1.847 | 0,030 | 8 / 8 | — | — |
| 48115 | `VCS_PHILC1` / `VCS_PHILC1` | Gang | 0,169 | 0,170 | 1.299 | 1.932 | 0,040 | 8 / 8 | — | — |
| 48116 | `VCS_ROBBER` / `VCS_ROBBER` | Cảnh sát / quân đội / cứu hộ | 0,103 | 0,105 | 961 | 1.424 | 0,006 | 5 / 7 | — | — |
| 48117 | `VCS_SARGE` / `VCS_SARGE` | Gang | 0,075 | 0,078 | 1.094 | 781 | 0,007 | 8 / 8 | — | — |
| 48118 | `VCS_SHOPKPR` / `VCS_SHOPKPR` | Dân thường | 0,112 | 0,113 | 1.019 | 1.490 | 0,011 | 7 / 8 | — | — |
| 48119 | `VCS_SWAT` / `VCS_SWAT` | Cảnh sát / quân đội / cứu hộ | 0,128 | 0,131 | 1.192 | 1.751 | 0,009 | 9 / 9 | Vice City | — |
| 48120 | `VCS_VICE1` / `VCS_VICE1` | Cảnh sát / quân đội / cứu hộ | 0,123 | 0,125 | 961 | 1.395 | 0,027 | 7 / 7 | — | Tên texture cần xác minh: vice2_shoe |
| 48121 | `VCS_VICE2` / `VCS_VICE2` | Cảnh sát / quân đội / cứu hộ | 0,109 | 0,109 | 1.025 | 1.463 | 0,009 | 7 / 7 | — | — |
| 48122 | `VCS_WFOBE` / `VCS_WFOBE` | Dân thường | 0,110 | 0,111 | 1.026 | 1.456 | 0,010 | 7 / 7 | Vice City | — |
| 48123 | `VCS_WFOGO` / `VCS_WFOGO` | Dân thường | 0,108 | 0,111 | 990 | 1.398 | 0,011 | 7 / 10 | — | — |
| 48124 | `VCS_WFORI` / `VCS_WFORI` | Dân thường | 0,110 | 0,111 | 1.026 | 1.543 | 0,006 | 6 / 6 | Vice City | — |
| 48125 | `VCS_WFOSH` / `VCS_WFOSH` | Dân thường | 0,117 | 0,119 | 1.094 | 1.601 | 0,008 | 7 / 8 | Vice City | — |
| 48126 | `VCS_WFOST` / `VCS_WFOST` | Dân thường | 0,111 | 0,113 | 1.046 | 1.522 | 0,007 | 6 / 7 | — | — |
| 48127 | `VCS_WFOTR` / `VCS_WFOTR` | Dân thường | 0,106 | 0,109 | 944 | 1.434 | 0,009 | 5 / 6 | — | — |
| 48128 | `VCS_WFYBE` / `VCS_WFYBE` | Dân thường | 0,109 | 0,109 | 1.036 | 1.493 | 0,007 | 6 / 7 | — | — |
| 48129 | `VCS_WFYBU` / `VCS_WFYBU` | Dân thường | 0,106 | 0,109 | 992 | 1.443 | 0,007 | 7 / 7 | Vice City | — |
| 48130 | `VCS_WFYJG` / `VCS_WFYJG` | Dân thường | 0,107 | 0,109 | 1.000 | 1.462 | 0,007 | 6 / 8 | — | — |
| 48131 | `VCS_WFYLG` / `VCS_WFYLG` | Dân thường | 0,117 | 0,117 | 1.080 | 1.595 | 0,009 | 6 / 6 | Vice City | — |
| 48132 | `VCS_WFYPR` / `VCS_WFYPR` | Prostitute | 0,109 | 0,111 | 1.026 | 1.497 | 0,007 | 5 / 6 | — | — |
| 48133 | `VCS_WFYRI` / `VCS_WFYRI` | Dân thường | 0,108 | 0,109 | 1.022 | 1.509 | 0,006 | 6 / 6 | Vice City | P1 |
| 48134 | `VCS_WFYSH` / `VCS_WFYSH` | Dân thường | 0,116 | 0,119 | 1.056 | 1.536 | 0,011 | 8 / 9 | Vice City | — |
| 48135 | `VCS_WFYSK` / `VCS_WFYSK` | Dân thường | 0,114 | 0,117 | 1.054 | 1.541 | 0,009 | 6 / 7 | Vice City | — |
| 48136 | `VCS_WFYST` / `VCS_WFYST` | Dân thường | 0,132 | 0,133 | 982 | 1.463 | 0,032 | 8 / 8 | Vice City | — |
| 48137 | `VCS_WMOBE` / `VCS_WMOBE` | Dân thường | 0,105 | 0,107 | 932 | 1.386 | 0,010 | 7 / 7 | Vice City | — |
| 48138 | `VCS_WMOBU` / `VCS_WMOBU` | Dân thường | 0,109 | 0,111 | 947 | 1.374 | 0,015 | 6 / 7 | Vice City | — |
| 48139 | `VCS_WMOCA` / `VCS_WMOCA` | Dân thường | 0,096 | 0,100 | 889 | 1.291 | 0,007 | 7 / 7 | Vice City | — |
| 48140 | `VCS_WMOGO` / `VCS_WMOGO` | Dân thường | 0,104 | 0,105 | 928 | 1.381 | 0,009 | 8 / 8 | — | — |
| 48141 | `VCS_WMORI` / `VCS_WMORI` | Dân thường | 0,106 | 0,109 | 975 | 1.413 | 0,009 | 6 / 6 | Vice City | — |
| 48142 | `VCS_WMOST` / `VCS_WMOST` | Dân thường | 0,105 | 0,107 | 943 | 1.382 | 0,010 | 7 / 7 | — | — |
| 48143 | `VCS_WMOTR` / `VCS_WMOTR` | Dân thường | 0,109 | 0,109 | 954 | 1.457 | 0,010 | 4 / 5 | — | — |
| 48144 | `VCS_WMYBE` / `VCS_WMYBE` | Dân thường | 0,110 | 0,111 | 1.008 | 1.453 | 0,010 | 6 / 8 | Vice City | — |
| 48145 | `VCS_WMYBU` / `VCS_WMYBU` | Dân thường | 0,113 | 0,115 | 1.044 | 1.545 | 0,008 | 7 / 8 | Vice City | — |
| 48146 | `VCS_WMYCR` / `VCS_WMYCR` | Criminal | 0,105 | 0,105 | 953 | 1.413 | 0,008 | 7 / 7 | Vice City | — |
| 48147 | `VCS_WMYCW` / `VCS_WMYCW` | Dân thường | 0,106 | 0,107 | 990 | 1.425 | 0,008 | 8 / 8 | — | — |
| 48148 | `VCS_WMYJG` / `VCS_WMYJG` | Dân thường | 0,113 | 0,115 | 1.014 | 1.484 | 0,012 | 8 / 9 | — | — |
| 48149 | `VCS_WMYLG` / `VCS_WMYLG` | Dân thường | 0,110 | 0,111 | 1.008 | 1.427 | 0,012 | 7 / 7 | Vice City | — |
| 48150 | `VCS_WMYPI` / `VCS_WMYPI` | Criminal | 0,118 | 0,121 | 1.030 | 1.500 | 0,014 | 10 / 11 | Vice City | — |
| 48151 | `VCS_WMYRI` / `VCS_WMYRI` | Dân thường | 0,101 | 0,104 | 955 | 1.385 | 0,006 | 6 / 6 | Vice City | P1 |
| 48152 | `VCS_WMYSK` / `VCS_WMYSK` | Dân thường | 0,120 | 0,121 | 1.102 | 1.588 | 0,012 | 6 / 7 | Vice City | — |
| 48153 | `VCS_WMYST` / `VCS_WMYST` | Dân thường | 0,117 | 0,119 | 1.022 | 1.549 | 0,012 | 7 / 7 | Vice City | — |
| 48154 | `VCS_ZOMA` / `VCS_ZOMA` | Gang | 0,111 | 0,113 | 987 | 1.536 | 0,009 | 5 / 5 | — | — |
| 48155 | `LCS_BIKER01` / `LCS_BIKER01` | Gang | 0,139 | 0,141 | 1.166 | 1.666 | 0,025 | 9 / 9 | — | — |
| 48156 | `LCS_BIKER02` / `LCS_BIKER02` | Gang | 0,115 | 0,117 | 1.026 | 1.460 | 0,015 | 7 / 7 | — | — |
| 48157 | `LCS_BIKER03` / `LCS_BIKER03` | Gang | 0,116 | 0,117 | 1.034 | 1.484 | 0,015 | 7 / 7 | — | — |
| 48158 | `LCS_BIKER04` / `LCS_BIKER04` | Gang | 0,177 | 0,180 | 1.582 | 2.361 | 0,021 | 10 / 10 | — | — |
| 48159 | `LCS_CAS_WOM` / `LCS_CAS_WOM` | Dân thường | 0,063 | 0,064 | 846 | 602 | 0,010 | 1 / 1 | — | — |
| 48160 | `LCS_COLUMBIAN01` / `LCS_COLUMBIAN01` | Gang | 0,124 | 0,127 | 1.163 | 1.722 | 0,008 | 8 / 8 | — | — |
| 48161 | `LCS_COLUMBIAN02` / `LCS_COLUMBIAN02` | Gang | 0,121 | 0,123 | 1.141 | 1.656 | 0,008 | 8 / 8 | — | — |
| 48162 | `LCS_CONST1` / `LCS_CONST1` | Dân thường | 0,105 | 0,107 | 1.444 | 1.114 | 0,016 | 2 / 3 | — | — |
| 48163 | `LCS_CONST2` / `LCS_CONST2` | Dân thường | 0,100 | 0,102 | 1.351 | 1.026 | 0,016 | 2 / 5 | — | — |
| 48164 | `LCS_CRIMINAL01` / `LCS_CRIMINAL01` | Criminal | 0,075 | 0,076 | 1.016 | 765 | 0,011 | 2 / 4 | — | — |
| 48165 | `LCS_CRIMINAL02` / `LCS_CRIMINAL02` | Criminal | 0,075 | 0,076 | 994 | 768 | 0,011 | 2 / 2 | — | — |
| 48166 | `LCS_CSCHERYL` / `LCS_CSCHERYL` | Dân thường | 0,168 | 0,170 | 2.096 | 1.600 | 0,042 | 1 / 1 | — | — |
| 48167 | `LCS_CSGIMP` / `LCS_CSGIMP` | Dân thường | 0,220 | 0,221 | 2.738 | 2.401 | 0,042 | 1 / 1 | — | — |
| 48168 | `LCS_CSGUARD` / `LCS_CSGUARD` | Dân thường | 0,135 | 0,139 | 1.696 | 1.307 | 0,031 | 2 / 2 | — | — |
| 48169 | `LCS_CSHOBO` / `LCS_CSHOBO` | Dân thường | 0,159 | 0,160 | 1.800 | 1.320 | 0,052 | 2 / 2 | — | — |
| 48170 | `LCS_CSKAS` / `LCS_CSKAS` | Dân thường | 0,175 | 0,178 | 2.349 | 1.658 | 0,042 | 1 / 1 | — | — |
| 48171 | `LCS_CSLOVE` / `LCS_CSLOVE` | Dân thường | 0,163 | 0,164 | 1.862 | 1.383 | 0,052 | 2 / 2 | — | — |
| 48172 | `LCS_CSMAC` / `LCS_CSMAC` | Dân thường | 0,152 | 0,152 | 1.566 | 1.264 | 0,052 | 2 / 2 | — | — |
| 48173 | `LCS_CSMAR` / `LCS_CSMAR` | Dân thường | 0,171 | 0,174 | 2.134 | 1.663 | 0,042 | 1 / 1 | — | — |
| 48174 | `LCS_CSMARB` / `LCS_CSMARB` | Dân thường | 0,171 | 0,174 | 2.134 | 1.663 | 0,042 | 1 / 1 | — | — |
| 48175 | `LCS_CSRAY` / `LCS_CSRAY` | Dân thường | 0,157 | 0,158 | 1.654 | 1.332 | 0,052 | 2 / 2 | — | — |
| 48176 | `LCS_CSSAL` / `LCS_CSSAL` | Dân thường | 0,166 | 0,168 | 1.866 | 1.439 | 0,052 | 2 / 2 | — | — |
| 48177 | `LCS_CSSALP` / `LCS_CSSALP` | Dân thường | 0,149 | 0,150 | 1.834 | 1.464 | 0,033 | 7 / 7 | — | — |
| 48178 | `LCS_CSTOOL` / `LCS_CSTOOL` | Dân thường | 0,187 | 0,189 | 2.238 | 1.728 | 0,052 | 2 / 2 | — | — |
| 48179 | `LCS_CSUNCLE` / `LCS_CSUNCLE` | Dân thường | 0,188 | 0,189 | 2.145 | 1.787 | 0,052 | 2 / 2 | — | — |
| 48180 | `LCS_CSVINC` / `LCS_CSVINC` | Dân thường | 0,205 | 0,207 | 1.548 | 2.353 | 0,052 | 2 / 2 | — | — |
| 48181 | `LCS_CT_MAN1` / `LCS_CT_MAN1` | Dân thường | 0,069 | 0,072 | 938 | 693 | 0,010 | 1 / 1 | — | — |
| 48182 | `LCS_CT_MAN2` / `LCS_CT_MAN2` | Dân thường | 0,106 | 0,107 | 986 | 1.421 | 0,009 | 6 / 6 | — | — |
| 48183 | `LCS_CT_WOM1` / `LCS_CT_WOM1` | Dân thường | 0,059 | 0,061 | 862 | 593 | 0,006 | 4 / 4 | — | — |
| 48184 | `LCS_CT_WOM2` / `LCS_CT_WOM2` | Dân thường | 0,061 | 0,062 | 914 | 605 | 0,006 | 4 / 4 | — | — |
| 48185 | `LCS_DELIASS` / `LCS_DELIASS` | Dân thường | 0,080 | 0,082 | 1.008 | 774 | 0,013 | 9 / 9 | — | — |
| 48186 | `LCS_DIABLO01` / `LCS_DIABLO01` | Gang | 0,167 | 0,170 | 1.708 | 2.401 | 0,007 | 5 / 5 | — | — |
| 48187 | `LCS_DIABLO02` / `LCS_DIABLO02` | Gang | 0,168 | 0,170 | 1.726 | 2.413 | 0,007 | 6 / 6 | — | — |
| 48188 | `LCS_DOCKER1` / `LCS_DOCKER1` | Dân thường | 0,086 | 0,088 | 1.348 | 915 | 0,007 | 7 / 7 | — | — |
| 48189 | `LCS_DOCKER2` / `LCS_DOCKER2` | Dân thường | 0,092 | 0,094 | 1.416 | 976 | 0,009 | 7 / 7 | — | — |
| 48190 | `LCS_DONOVAN` / `LCS_DONOVAN` | Dân thường | 0,204 | 0,207 | 1.768 | 2.682 | 0,031 | 1 / 1 | — | — |
| 48191 | `LCS_FAN_MAN1` / `LCS_FAN_MAN1` | Dân thường | 0,074 | 0,076 | 1.032 | 741 | 0,010 | 8 / 8 | — | — |
| 48192 | `LCS_FAN_MAN2` / `LCS_FAN_MAN2` | Dân thường | 0,071 | 0,074 | 1.036 | 718 | 0,008 | 7 / 7 | — | — |
| 48193 | `LCS_FAN_WOM` / `LCS_FAN_WOM` | Dân thường | 0,068 | 0,070 | 966 | 676 | 0,008 | 6 / 6 | — | — |
| 48194 | `LCS_FATFEMALE01` / `LCS_FATFEMALE01` | Dân thường | 0,068 | 0,070 | 909 | 704 | 0,008 | 5 / 5 | — | — |
| 48195 | `LCS_FATFEMALE02` / `LCS_FATFEMALE02` | Dân thường | 0,064 | 0,066 | 850 | 682 | 0,006 | 4 / 4 | — | — |
| 48196 | `LCS_FATMALE01` / `LCS_FATMALE01` | Dân thường | 0,058 | 0,061 | 855 | 563 | 0,006 | 6 / 7 | — | — |
| 48197 | `LCS_FATMALE02` / `LCS_FATMALE02` | Dân thường | 0,064 | 0,066 | 902 | 660 | 0,006 | 7 / 7 | — | — |
| 48198 | `LCS_FEMALE01` / `LCS_FEMALE01` | Dân thường | 0,086 | 0,088 | 1.201 | 954 | 0,008 | 6 / 6 | — | — |
| 48199 | `LCS_FEMALE02` / `LCS_FEMALE02` | Dân thường | 0,084 | 0,088 | 1.064 | 848 | 0,016 | 1 / 1 | — | — |
| 48200 | `LCS_FEMALE03` / `LCS_FEMALE03` | Dân thường | 0,100 | 0,102 | 1.565 | 1.108 | 0,008 | 4 / 4 | — | — |
| 48201 | `LCS_FIREMAN` / `LCS_FIREMAN` | Cảnh sát / quân đội / cứu hộ | 0,147 | 0,150 | 1.464 | 2.091 | 0,007 | 6 / 6 | — | — |
| 48202 | `LCS_FORELLI1` / `LCS_FORELLI1` | Gang | 0,091 | 0,092 | 844 | 1.175 | 0,009 | 6 / 6 | — | — |
| 48203 | `LCS_FORELLI2` / `LCS_FORELLI2` | Gang | 0,091 | 0,092 | 844 | 1.175 | 0,009 | 6 / 6 | — | — |
| 48204 | `LCS_GRDANG1` / `LCS_GRDANG1` | Dân thường | 0,126 | 0,129 | 1.182 | 1.716 | 0,010 | 8 / 8 | — | — |
| 48205 | `LCS_GRDANG2` / `LCS_GRDANG2` | Dân thường | 0,092 | 0,094 | 1.326 | 944 | 0,011 | 10 / 10 | — | — |
| 48206 | `LCS_GUN_ASS` / `LCS_GUN_ASS` | Dân thường | 0,116 | 0,117 | 1.034 | 1.484 | 0,015 | 7 / 7 | — | — |
| 48207 | `LCS_HOLEJOG` / `LCS_HOLEJOG` | Dân thường | 0,077 | 0,078 | 1.095 | 810 | 0,008 | 6 / 6 | — | — |
| 48208 | `LCS_HOPPER` / `LCS_HOPPER` | Dân thường | 0,088 | 0,090 | 1.134 | 1.011 | 0,008 | 9 / 9 | — | — |
| 48209 | `LCS_HOS_MAN` / `LCS_HOS_MAN` | Cảnh sát / quân đội / cứu hộ | 0,075 | 0,076 | 1.060 | 779 | 0,009 | 6 / 6 | — | — |
| 48210 | `LCS_HOS_WOM` / `LCS_HOS_WOM` | Cảnh sát / quân đội / cứu hộ | 0,086 | 0,088 | 1.136 | 939 | 0,009 | 7 / 7 | — | — |
| 48211 | `LCS_KAZUKI` / `LCS_KAZUKI` | Dân thường | 0,111 | 0,113 | 1.511 | 1.189 | 0,016 | 3 / 3 | — | — |
| 48212 | `LCS_LEONE01` / `LCS_LEONE01` | Gang | 0,137 | 0,139 | 1.334 | 1.927 | 0,007 | 7 / 7 | — | — |
| 48213 | `LCS_LEONE02` / `LCS_LEONE02` | Gang | 0,199 | 0,201 | 2.016 | 2.918 | 0,007 | 7 / 7 | — | — |
| 48214 | `LCS_LI_MAN1` / `LCS_LI_MAN1` | Dân thường | 0,072 | 0,074 | 1.128 | 759 | 0,006 | 5 / 5 | — | — |
| 48215 | `LCS_LI_MAN2` / `LCS_LI_MAN2` | Dân thường | 0,100 | 0,104 | 1.615 | 1.130 | 0,006 | 5 / 5 | — | — |
| 48216 | `LCS_LI_WOM1` / `LCS_LI_WOM1` | Dân thường | 0,067 | 0,070 | 963 | 687 | 0,007 | 5 / 5 | — | — |
| 48217 | `LCS_LI_WOM2` / `LCS_LI_WOM2` | Dân thường | 0,068 | 0,068 | 974 | 704 | 0,007 | 5 / 5 | — | — |
| 48218 | `LCS_M_HOLE` / `LCS_M_HOLE` | Dân thường | 0,129 | 0,131 | 1.132 | 1.631 | 0,018 | 9 / 9 | — | — |
| 48219 | `LCS_MALE01` / `LCS_MALE01` | Dân thường | 0,077 | 0,078 | 1.174 | 796 | 0,007 | 5 / 5 | — | — |
| 48220 | `LCS_MALE02` / `LCS_MALE02` | Dân thường | 0,073 | 0,074 | 1.030 | 736 | 0,009 | 6 / 6 | — | — |
| 48221 | `LCS_MALE03` / `LCS_MALE03` | Dân thường | 0,064 | 0,066 | 850 | 642 | 0,008 | 6 / 8 | — | — |
| 48222 | `LCS_MASTOR` / `LCS_MASTOR` | Dân thường | 0,100 | 0,102 | 1.358 | 1.100 | 0,013 | 2 / 2 | — | — |
| 48223 | `LCS_MICKEYH` / `LCS_MICKEYH` | Gang | 0,128 | 0,131 | 1.820 | 1.422 | 0,015 | 8 / 8 | — | — |
| 48224 | `LCS_MIGUEL` / `LCS_MIGUEL` | Dân thường | 0,083 | 0,084 | 1.112 | 837 | 0,012 | 8 / 8 | — | — |
| 48225 | `LCS_MOD_MAN` / `LCS_MOD_MAN` | Dân thường | 0,088 | 0,090 | 1.359 | 944 | 0,008 | 7 / 7 | — | — |
| 48226 | `LCS_MOD_WOM` / `LCS_MOD_WOM` | Dân thường | 0,055 | 0,059 | 757 | 560 | 0,005 | 6 / 6 | — | — |
| 48227 | `LCS_NED_01` / `LCS_NED_01` | Dân thường | 0,115 | 0,115 | 1.690 | 1.237 | 0,012 | 8 / 9 | — | Tên texture cần xác minh: ciggie |
| 48228 | `LCS_P_MAN1` / `LCS_P_MAN1` | Dân thường | 0,066 | 0,068 | 948 | 660 | 0,007 | 6 / 6 | — | — |
| 48229 | `LCS_P_MAN2` / `LCS_P_MAN2` | Dân thường | 0,108 | 0,109 | 1.658 | 1.257 | 0,006 | 6 / 6 | — | — |
| 48230 | `LCS_P_WOM1` / `LCS_P_WOM1` | Dân thường | 0,061 | 0,062 | 862 | 634 | 0,005 | 7 / 7 | — | — |
| 48231 | `LCS_P_WOM2` / `LCS_P_WOM2` | Dân thường | 0,069 | 0,070 | 1.024 | 714 | 0,007 | 5 / 5 | — | — |
| 48232 | `LCS_PAULIE` / `LCS_PAULIE` | Dân thường | 0,082 | 0,084 | 1.016 | 712 | 0,019 | 7 / 7 | — | — |
| 48233 | `LCS_PHIL` / `LCS_PHIL` | Dân thường | 0,080 | 0,082 | 997 | 849 | 0,010 | 7 / 9 | — | — |
| 48234 | `LCS_PIMP` / `LCS_PIMP` | Dân thường | 0,095 | 0,096 | 1.385 | 1.011 | 0,010 | 7 / 7 | — | — |
| 48235 | `LCS_PMAN2` / `LCS_PMAN2` | Dân thường | 0,069 | 0,072 | 921 | 725 | 0,007 | 7 / 7 | — | — |
| 48236 | `LCS_PROSTITUTE` / `LCS_PROSTITUTE` | Prostitute | 0,071 | 0,072 | 972 | 769 | 0,006 | 8 / 8 | — | — |
| 48237 | `LCS_PROSTITUTE2` / `LCS_PROSTITUTE2` | Prostitute | 0,069 | 0,070 | 1.030 | 731 | 0,005 | 8 / 8 | — | — |
| 48238 | `LCS_SCUM_MAN` / `LCS_SCUM_MAN` | Dân thường | 0,066 | 0,068 | 933 | 694 | 0,006 | 6 / 6 | — | — |
| 48239 | `LCS_SCUM_WOM` / `LCS_SCUM_WOM` | Dân thường | 0,069 | 0,070 | 1.011 | 722 | 0,006 | 4 / 4 | — | — |
| 48240 | `LCS_SHOPPER1` / `LCS_SHOPPER1` | Dân thường | 0,110 | 0,111 | 1.627 | 1.303 | 0,007 | 7 / 7 | — | — |
| 48241 | `LCS_SHOPPER2` / `LCS_SHOPPER2` | Dân thường | 0,063 | 0,064 | 838 | 660 | 0,007 | 5 / 5 | — | — |
| 48242 | `LCS_SHOPPER3` / `LCS_SHOPPER3` | Dân thường | 0,091 | 0,092 | 1.372 | 1.013 | 0,006 | 7 / 7 | — | — |
| 48243 | `LCS_SINDACCO01` / `LCS_SINDACCO01` | Gang | 0,173 | 0,176 | 1.702 | 2.442 | 0,011 | 7 / 7 | — | — |
| 48244 | `LCS_SINDACCO02` / `LCS_SINDACCO02` | Gang | 0,171 | 0,172 | 1.706 | 2.413 | 0,011 | 7 / 7 | — | — |
| 48245 | `LCS_SINDACCO03` / `LCS_SINDACCO03` | Gang | 0,735 | 0,736 | 1.984 | 3.180 | 0,531 | 6 / 6 | — | — |
| 48246 | `LCS_ST_MAN` / `LCS_ST_MAN` | Dân thường | 0,069 | 0,070 | 959 | 696 | 0,008 | 7 / 7 | — | — |
| 48247 | `LCS_ST_WOM` / `LCS_ST_WOM` | Dân thường | 0,063 | 0,064 | 876 | 661 | 0,006 | 6 / 6 | — | — |
| 48248 | `LCS_STUD_MAN` / `LCS_STUD_MAN` | Gang | 0,090 | 0,094 | 1.361 | 947 | 0,009 | 7 / 7 | — | — |
| 48249 | `LCS_STUD_WOM` / `LCS_STUD_WOM` | Gang | 0,080 | 0,082 | 1.222 | 826 | 0,007 | 7 / 7 | — | — |
| 48250 | `LCS_TAXI_D` / `LCS_TAXI_D` | Dân thường | 0,062 | 0,064 | 866 | 632 | 0,006 | 7 / 7 | — | — |
| 48251 | `LCS_THUG_01` / `LCS_THUG_01` | Dân thường | 0,078 | 0,080 | 1.054 | 778 | 0,011 | 7 / 8 | — | — |
| 48252 | `LCS_THUG_02` / `LCS_THUG_02` | Dân thường | 0,080 | 0,082 | 1.068 | 796 | 0,011 | 7 / 8 | — | — |
| 48253 | `LCS_WOM3` / `LCS_WOM3` | Dân thường | 0,071 | 0,074 | 980 | 759 | 0,008 | 2 / 2 | — | — |
| 48254 | `LCS_WORKER1` / `LCS_WORKER1` | Dân thường | 0,066 | 0,068 | 938 | 660 | 0,008 | 6 / 6 | — | — |
| 48255 | `LCS_WORKER2` / `LCS_WORKER2` | Dân thường | 0,101 | 0,104 | 1.485 | 1.138 | 0,009 | 6 / 6 | — | — |
| 48256 | `LCS_YAKUZA01` / `LCS_YAKUZA01` | Gang | 0,102 | 0,104 | 938 | 1.329 | 0,010 | 7 / 7 | — | — |
| 48257 | `LCS_YAKUZA02` / `LCS_YAKUZA02` | Gang | 0,100 | 0,102 | 910 | 1.290 | 0,010 | 7 / 7 | — | — |
| 48258 | `VC_APOULET` / `VC_APOULET` | Dân thường | 0,189 | 0,191 | 2.308 | 1.960 | 0,042 | 1 / 1 | — | — |
| 48259 | `VC_ARMY` / `VC_ARMY` | Cảnh sát / quân đội / cứu hộ | 0,083 | 0,086 | 1.012 | 840 | 0,016 | 1 / 1 | Vice City | — |
| 48260 | `VC_AVERY` / `VC_AVERY` | Dân thường | 0,201 | 0,203 | 2.788 | 2.011 | 0,042 | 1 / 1 | — | — |
| 48261 | `VC_BFOBE` / `VC_BFOBE` | Dân thường | 0,076 | 0,078 | 876 | 652 | 0,021 | 1 / 1 | Vice City | — |
| 48262 | `VC_BFORI` / `VC_BFORI` | Dân thường | 0,088 | 0,090 | 1.008 | 840 | 0,021 | 1 / 1 | Vice City | — |
| 48263 | `VC_BFOST` / `VC_BFOST` | Dân thường | 0,092 | 0,094 | 1.033 | 908 | 0,021 | 1 / 1 | — | — |
| 48264 | `VC_BFOTR` / `VC_BFOTR` | Dân thường | 0,088 | 0,090 | 996 | 837 | 0,021 | 1 / 1 | — | — |
| 48265 | `VC_BFYBE` / `VC_BFYBE` | Dân thường | 0,081 | 0,082 | 986 | 705 | 0,021 | 1 / 1 | Vice City | P1 |
| 48266 | `VC_BFYPR` / `VC_BFYPR` | Prostitute | 0,083 | 0,084 | 963 | 746 | 0,021 | 1 / 1 | Vice City | — |
| 48267 | `VC_BFYRI` / `VC_BFYRI` | Dân thường | 0,086 | 0,088 | 995 | 798 | 0,021 | 1 / 1 | Vice City | — |
| 48268 | `VC_BFYST` / `VC_BFYST` | Dân thường | 0,087 | 0,088 | 970 | 829 | 0,021 | 1 / 1 | Vice City | — |
| 48269 | `VC_BGA` / `VC_BGA` | Dân thường | 0,093 | 0,096 | 974 | 1.048 | 0,016 | 1 / 1 | — | — |
| 48270 | `VC_BGB` / `VC_BGB` | Dân thường | 0,096 | 0,098 | 952 | 1.018 | 0,021 | 1 / 1 | — | — |
| 48271 | `VC_BIKER01` / `VC_BIKER01` | Gang | 0,089 | 0,090 | 959 | 881 | 0,021 | 1 / 1 | Vice City | — |
| 48272 | `VC_BIKER02` / `VC_BIKER02` | Gang | 0,087 | 0,088 | 960 | 829 | 0,021 | 1 / 1 | Vice City | — |
| 48273 | `VC_BMOBE` / `VC_BMOBE` | Dân thường | 0,081 | 0,082 | 902 | 744 | 0,021 | 1 / 1 | Vice City | — |
| 48274 | `VC_BMODK` / `VC_BMODK` | Dân thường | 0,093 | 0,094 | 972 | 944 | 0,021 | 1 / 1 | Vice City | — |
| 48275 | `VC_BMOST` / `VC_BMOST` | Dân thường | 0,109 | 0,109 | 1.084 | 1.227 | 0,021 | 1 / 1 | Vice City | — |
| 48276 | `VC_BMOTR` / `VC_BMOTR` | Dân thường | 0,096 | 0,098 | 956 | 1.013 | 0,021 | 1 / 1 | Vice City | — |
| 48277 | `VC_BMYBB` / `VC_BMYBB` | Dân thường | 0,095 | 0,096 | 996 | 978 | 0,021 | 1 / 1 | Vice City | — |
| 48278 | `VC_BMYBE` / `VC_BMYBE` | Dân thường | 0,077 | 0,078 | 876 | 659 | 0,021 | 1 / 1 | Vice City | — |
| 48279 | `VC_BMYBU` / `VC_BMYBU` | Dân thường | 0,101 | 0,102 | 1.038 | 1.084 | 0,021 | 1 / 1 | Vice City | P1 |
| 48280 | `VC_BMYCR` / `VC_BMYCR` | Criminal | 0,095 | 0,096 | 984 | 979 | 0,021 | 1 / 1 | Vice City | — |
| 48281 | `VC_BMYPI` / `VC_BMYPI` | Dân thường | 0,104 | 0,105 | 1.045 | 1.137 | 0,021 | 1 / 1 | Vice City | — |
| 48282 | `VC_BMYRI` / `VC_BMYRI` | Dân thường | 0,099 | 0,100 | 984 | 1.062 | 0,021 | 1 / 1 | Vice City | P1 |
| 48283 | `VC_BMYST` / `VC_BMYST` | Dân thường | 0,097 | 0,100 | 982 | 1.036 | 0,021 | 1 / 1 | Vice City | P1 |
| 48284 | `VC_BUDDY` / `VC_BUDDY` | Gang | 0,115 | 0,117 | 1.010 | 954 | 0,042 | 1 / 1 | — | — |
| 48285 | `VC_BURGER` / `VC_BURGER` | Dân thường | 0,086 | 0,088 | 954 | 820 | 0,021 | 1 / 1 | — | — |
| 48286 | `VC_C_WORKER` / `VC_C_WORKER` | Gang | 0,093 | 0,096 | 962 | 961 | 0,021 | 1 / 1 | — | — |
| 48287 | `VC_CHEF` / `VC_CHEF` | Gang | 0,108 | 0,109 | 1.367 | 1.097 | 0,021 | 1 / 1 | — | — |
| 48288 | `VC_COLONEL` / `VC_COLONEL` | Gang | 0,191 | 0,193 | 2.449 | 2.155 | 0,031 | 1 / 1 | — | — |
| 48289 | `VC_COP` / `VC_COP` | Cảnh sát / quân đội / cứu hộ | 0,094 | 0,096 | 996 | 951 | 0,021 | 1 / 1 | Vice City | — |
| 48290 | `VC_CSDEAL` / `VC_CSDEAL` | Model có pedtype PLAYER1/2 | 0,181 | 0,184 | 2.280 | 1.808 | 0,042 | 1 / 1 | — | — |
| 48291 | `VC_CSPAPA` / `VC_CSPAPA` | Dân thường | 0,128 | 0,129 | 1.244 | 1.122 | 0,042 | 1 / 1 | — | — |
| 48292 | `VC_CUBAN01` / `VC_CUBAN01` | Gang | 0,089 | 0,090 | 950 | 878 | 0,021 | 1 / 1 | Vice City | — |
| 48293 | `VC_CUBAN02` / `VC_CUBAN02` | Gang | 0,096 | 0,098 | 1.000 | 998 | 0,021 | 1 / 1 | Vice City | — |
| 48294 | `VC_DGOON1` / `VC_DGOON1` | Gang | 0,105 | 0,107 | 1.178 | 912 | 0,031 | 1 / 1 | Vice City | — |
| 48295 | `VC_DIAZ01` / `VC_DIAZ01` | Gang | 0,093 | 0,096 | 962 | 961 | 0,021 | 1 / 1 | Vice City | — |
| 48296 | `VC_DIAZ02` / `VC_DIAZ02` | Gang | 0,091 | 0,094 | 978 | 1.005 | 0,016 | 1 / 1 | Vice City | — |
| 48297 | `VC_FBI` / `VC_FBI` | Cảnh sát / quân đội / cứu hộ | 0,101 | 0,104 | 1.013 | 1.103 | 0,021 | 1 / 1 | Vice City | — |
| 48298 | `VC_FIREMEN` / `VC_FIREMEN` | Cảnh sát / quân đội / cứu hộ | 0,099 | 0,102 | 976 | 855 | 0,031 | 1 / 1 | Vice City | — |
| 48299 | `VC_FSFA` / `VC_FSFA` | Gang | 0,102 | 0,104 | 1.000 | 1.129 | 0,021 | 1 / 1 | — | — |
| 48300 | `VC_GDA` / `VC_GDA` | Cảnh sát / quân đội / cứu hộ | 0,084 | 0,086 | 963 | 770 | 0,021 | 1 / 1 | Vice City | — |
| 48301 | `VC_GDB` / `VC_GDB` | Cảnh sát / quân đội / cứu hộ | 0,079 | 0,082 | 963 | 770 | 0,016 | 1 / 1 | Vice City | — |
| 48302 | `VC_HAITIAN01` / `VC_HAITIAN01` | Gang | 0,093 | 0,096 | 992 | 952 | 0,021 | 1 / 1 | Vice City | — |
| 48303 | `VC_HAITIAN02` / `VC_HAITIAN02` | Gang | 0,097 | 0,100 | 1.008 | 1.022 | 0,021 | 1 / 1 | Vice City | — |
| 48304 | `VC_HAITIAN03` / `VC_HAITIAN03` | Gang | 0,105 | 0,107 | 978 | 983 | 0,031 | 1 / 1 | — | — |
| 48305 | `VC_HFOBE` / `VC_HFOBE` | Dân thường | 0,079 | 0,080 | 876 | 695 | 0,021 | 1 / 1 | Vice City | — |
| 48306 | `VC_HFORI` / `VC_HFORI` | Dân thường | 0,088 | 0,090 | 993 | 850 | 0,021 | 1 / 1 | Vice City | P1 |
| 48307 | `VC_HFOST` / `VC_HFOST` | Dân thường | 0,088 | 0,090 | 996 | 837 | 0,021 | 1 / 1 | — | — |
| 48308 | `VC_HFOTR` / `VC_HFOTR` | Dân thường | 0,088 | 0,090 | 996 | 837 | 0,021 | 1 / 1 | Vice City | — |
| 48309 | `VC_HFYBE` / `VC_HFYBE` | Dân thường | 0,079 | 0,080 | 972 | 676 | 0,021 | 1 / 1 | Vice City | — |
| 48310 | `VC_HFYBU` / `VC_HFYBU` | Dân thường | 0,087 | 0,088 | 968 | 829 | 0,021 | 1 / 1 | Vice City | P1 |
| 48311 | `VC_HFYCG` / `VC_HFYCG` | Dân thường | 0,088 | 0,090 | 970 | 848 | 0,021 | 1 / 1 | — | — |
| 48312 | `VC_HFYMD` / `VC_HFYMD` | Dân thường | 0,083 | 0,084 | 963 | 746 | 0,021 | 1 / 1 | — | — |
| 48313 | `VC_HFYPR` / `VC_HFYPR` | Prostitute | 0,077 | 0,080 | 968 | 725 | 0,016 | 1 / 1 | — | — |
| 48314 | `VC_HFYRI` / `VC_HFYRI` | Dân thường | 0,083 | 0,084 | 907 | 775 | 0,021 | 1 / 1 | Vice City | — |
| 48315 | `VC_HFYST` / `VC_HFYST` | Dân thường | 0,085 | 0,086 | 942 | 797 | 0,021 | 1 / 1 | Vice City | — |
| 48316 | `VC_HMOBE` / `VC_HMOBE` | Dân thường | 0,081 | 0,082 | 902 | 744 | 0,021 | 1 / 1 | Vice City | — |
| 48317 | `VC_HMOCA` / `VC_HMOCA` | Dân thường | 0,093 | 0,094 | 1.030 | 918 | 0,021 | 1 / 1 | Vice City | — |
| 48318 | `VC_HMORI` / `VC_HMORI` | Dân thường | 0,098 | 0,100 | 988 | 1.045 | 0,021 | 1 / 1 | Vice City | P1 |
| 48319 | `VC_HMOST` / `VC_HMOST` | Dân thường | 0,095 | 0,098 | 956 | 1.005 | 0,021 | 1 / 1 | Vice City | P1 |
| 48320 | `VC_HMOTR` / `VC_HMOTR` | Dân thường | 0,096 | 0,098 | 956 | 1.011 | 0,021 | 1 / 1 | Vice City | — |
| 48321 | `VC_HMYAP` / `VC_HMYAP` | Dân thường | 0,093 | 0,096 | 980 | 953 | 0,021 | 1 / 1 | — | — |
| 48322 | `VC_HMYBE` / `VC_HMYBE` | Dân thường | 0,083 | 0,084 | 922 | 764 | 0,021 | 1 / 1 | Vice City | — |
| 48323 | `VC_HMYRI` / `VC_HMYRI` | Dân thường | 0,096 | 0,098 | 1.010 | 998 | 0,021 | 1 / 1 | Vice City | P1 |
| 48324 | `VC_HMYST` / `VC_HMYST` | Dân thường | 0,095 | 0,098 | 988 | 992 | 0,021 | 1 / 1 | Vice City | P1 |
| 48325 | `VC_JFOTO` / `VC_JFOTO` | Dân thường | 0,087 | 0,088 | 980 | 834 | 0,021 | 1 / 1 | Vice City | — |
| 48326 | `VC_JMOTO` / `VC_JMOTO` | Dân thường | 0,086 | 0,088 | 990 | 800 | 0,021 | 1 / 1 | Vice City | — |
| 48327 | `VC_KENTPAUL` / `VC_KENTPAUL` | Dân thường | 0,206 | 0,209 | 2.625 | 2.380 | 0,031 | 1 / 1 | — | — |
| 48328 | `VC_LAWYER` / `VC_LAWYER` | Gang | 0,124 | 0,127 | 1.232 | 1.058 | 0,042 | 1 / 1 | — | — |
| 48329 | `VC_MALE01` / `VC_MALE01` | Dân thường | 0,095 | 0,096 | 990 | 983 | 0,021 | 1 / 1 | Vice City | — |
| 48330 | `VC_MBA` / `VC_MBA` | Gang | 0,109 | 0,111 | 1.160 | 988 | 0,031 | 1 / 1 | — | — |
| 48331 | `VC_MBB` / `VC_MBB` | Gang | 0,121 | 0,123 | 1.168 | 1.026 | 0,042 | 1 / 1 | — | — |
| 48332 | `VC_MEDIC` / `VC_MEDIC` | Cảnh sát / quân đội / cứu hộ | 0,091 | 0,092 | 964 | 905 | 0,021 | 1 / 1 | Vice City | — |
| 48333 | `VC_PLAY10` / `VC_PLAY10` | Model có pedtype PLAYER1/2 | 0,161 | 0,164 | 2.154 | 1.665 | 0,031 | 1 / 1 | — | — |
| 48334 | `VC_PLAY11` / `VC_PLAY11` | Model có pedtype PLAYER1/2 | 0,167 | 0,170 | 2.130 | 1.796 | 0,031 | 1 / 1 | — | — |
| 48335 | `VC_PLAY12` / `VC_PLAY12` | Model có pedtype PLAYER1/2 | 0,143 | 0,145 | 1.554 | 1.354 | 0,039 | 2 / 2 | — | — |
| 48336 | `VC_PLAYER` / `VC_PLAYER` | Model có pedtype PLAYER1/2 | 0,169 | 0,172 | 2.262 | 1.783 | 0,031 | 1 / 1 | — | — |
| 48337 | `VC_PLAYER2` / `VC_PLAYER2` | Model có pedtype PLAYER1/2 | 0,194 | 0,197 | 2.545 | 2.169 | 0,031 | 1 / 1 | — | — |
| 48338 | `VC_PLAYER3` / `VC_PLAYER3` | Model có pedtype PLAYER1/2 | 0,167 | 0,170 | 2.124 | 1.789 | 0,031 | 1 / 1 | — | — |
| 48339 | `VC_PLAYER4` / `VC_PLAYER4` | Model có pedtype PLAYER1/2 | 0,169 | 0,172 | 2.167 | 1.813 | 0,031 | 1 / 1 | — | — |
| 48340 | `VC_PLAYER5` / `VC_PLAYER5` | Model có pedtype PLAYER1/2 | 0,162 | 0,164 | 2.094 | 1.701 | 0,031 | 1 / 1 | — | — |
| 48341 | `VC_PLAYER6` / `VC_PLAYER6` | Model có pedtype PLAYER1/2 | 0,172 | 0,174 | 2.182 | 1.858 | 0,031 | 1 / 1 | — | — |
| 48342 | `VC_PLAYER7` / `VC_PLAYER7` | Model có pedtype PLAYER1/2 | 0,181 | 0,184 | 2.348 | 1.988 | 0,031 | 1 / 1 | — | — |
| 48343 | `VC_PLAYER8` / `VC_PLAYER8` | Model có pedtype PLAYER1/2 | 0,183 | 0,186 | 2.352 | 2.033 | 0,031 | 1 / 1 | — | — |
| 48344 | `VC_PLAYER9` / `VC_PLAYER9` | Model có pedtype PLAYER1/2 | 0,204 | 0,207 | 2.597 | 2.358 | 0,031 | 1 / 1 | — | — |
| 48345 | `VC_PSYCHO` / `VC_PSYCHO` | Gang | 0,093 | 0,094 | 986 | 937 | 0,021 | 1 / 1 | — | — |
| 48346 | `VC_S_KEEP` / `VC_S_KEEP` | Dân thường | 0,097 | 0,100 | 1.035 | 1.015 | 0,021 | 1 / 1 | — | — |
| 48347 | `VC_SAM` / `VC_SAM` | Dân thường | 0,093 | 0,094 | 962 | 957 | 0,021 | 1 / 1 | — | — |
| 48348 | `VC_SHARK01` / `VC_SHARK01` | Gang | 0,095 | 0,096 | 988 | 975 | 0,021 | 1 / 1 | Vice City | — |
| 48349 | `VC_SHARK02` / `VC_SHARK02` | Gang | 0,095 | 0,096 | 982 | 989 | 0,021 | 1 / 1 | Vice City | — |
| 48350 | `VC_SHARK03` / `VC_SHARK03` | Gang | 0,087 | 0,088 | 910 | 857 | 0,021 | 1 / 1 | Vice City | — |
| 48351 | `VC_SONNYGOONA` / `VC_SOONYGOONA` | Gang | 0,118 | 0,121 | 1.130 | 974 | 0,042 | 1 / 1 | — | — |
| 48352 | `VC_SONNYGOONB` / `VC_SOONYGOONB` | Gang | 0,121 | 0,123 | 1.172 | 1.026 | 0,042 | 1 / 1 | — | — |
| 48353 | `VC_SPANDXA` / `VC_SPANDXA` | Dân thường | 0,087 | 0,088 | 950 | 828 | 0,021 | 1 / 1 | — | — |
| 48354 | `VC_SPANDXB` / `VC_SPANDXB` | Dân thường | 0,084 | 0,086 | 946 | 785 | 0,021 | 1 / 1 | — | — |
| 48355 | `VC_STRIPA` / `VC_STRIPA` | Gang | 0,122 | 0,123 | 1.368 | 1.380 | 0,021 | 1 / 1 | — | — |
| 48356 | `VC_STRIPB` / `VC_STRIPB` | Gang | 0,093 | 0,094 | 1.055 | 914 | 0,021 | 1 / 1 | — | — |
| 48357 | `VC_STRIPC` / `VC_STRIPC` | Gang | 0,093 | 0,094 | 1.081 | 910 | 0,021 | 1 / 1 | — | — |
| 48358 | `VC_SWAT` / `VC_SWAT` | Cảnh sát / quân đội / cứu hộ | 0,082 | 0,086 | 996 | 833 | 0,016 | 1 / 1 | Vice City | — |
| 48359 | `VC_TAXI_D` / `VC_TAXI_D` | Dân thường | 0,093 | 0,094 | 1.030 | 918 | 0,021 | 1 / 1 | Vice City | — |
| 48360 | `VC_VERCETTI01` / `VC_VERCETTI01` | Gang | 0,113 | 0,115 | 1.206 | 1.060 | 0,031 | 1 / 1 | Vice City | — |
| 48361 | `VC_VERCETTI02` / `VC_VERCETTI02` | Gang | 0,113 | 0,115 | 1.206 | 1.060 | 0,031 | 1 / 1 | Vice City | — |
| 48362 | `VC_VICE1` / `VC_VICE1` | Cảnh sát / quân đội / cứu hộ | 0,097 | 0,098 | 995 | 1.018 | 0,021 | 1 / 1 | — | — |
| 48363 | `VC_VICE2` / `VC_VICE2` | Cảnh sát / quân đội / cứu hộ | 0,102 | 0,104 | 1.042 | 1.110 | 0,021 | 1 / 1 | — | — |
| 48364 | `VC_VICE3` / `VC_VICE3` | Cảnh sát / quân đội / cứu hộ | 0,100 | 0,102 | 1.009 | 1.083 | 0,021 | 1 / 1 | — | — |
| 48365 | `VC_VICE4` / `VC_VICE4` | Cảnh sát / quân đội / cứu hộ | 0,094 | 0,096 | 982 | 970 | 0,021 | 1 / 1 | — | — |
| 48366 | `VC_VICE5` / `VC_VICE5` | Cảnh sát / quân đội / cứu hộ | 0,097 | 0,100 | 988 | 1.033 | 0,021 | 1 / 1 | — | — |
| 48367 | `VC_VICE6` / `VC_VICE6` | Cảnh sát / quân đội / cứu hộ | 0,097 | 0,100 | 962 | 1.041 | 0,021 | 1 / 1 | — | — |
| 48368 | `VC_VICE7` / `VC_VICE7` | Cảnh sát / quân đội / cứu hộ | 0,096 | 0,098 | 985 | 998 | 0,021 | 1 / 1 | — | — |
| 48369 | `VC_VICE8` / `VC_VICE8` | Cảnh sát / quân đội / cứu hộ | 0,097 | 0,100 | 990 | 1.030 | 0,021 | 1 / 1 | — | — |
| 48370 | `VC_WFOBE` / `VC_WFOBE` | Dân thường | 0,077 | 0,078 | 884 | 657 | 0,021 | 1 / 1 | — | — |
| 48371 | `VC_WFOGO` / `VC_WFOGO` | Dân thường | 0,085 | 0,086 | 978 | 784 | 0,021 | 1 / 1 | — | — |
| 48372 | `VC_WFORI` / `VC_WFORI` | Dân thường | 0,082 | 0,086 | 965 | 844 | 0,016 | 1 / 1 | Vice City | P1 |
| 48373 | `VC_WFOSH` / `VC_WFOSH` | Dân thường | 0,087 | 0,088 | 986 | 813 | 0,021 | 1 / 1 | — | — |
| 48374 | `VC_WFOST` / `VC_WFOST` | Dân thường | 0,087 | 0,090 | 987 | 924 | 0,016 | 1 / 1 | — | — |
| 48375 | `VC_WFOTR` / `VC_WFOTR` | Dân thường | 0,088 | 0,090 | 992 | 845 | 0,021 | 1 / 1 | — | — |
| 48376 | `VC_WFYBE` / `VC_WFYBE` | Dân thường | 0,078 | 0,078 | 950 | 647 | 0,021 | 1 / 1 | Vice City | — |
| 48377 | `VC_WFYBU` / `VC_WFYBU` | Dân thường | 0,088 | 0,090 | 978 | 848 | 0,021 | 1 / 1 | Vice City | P1 |
| 48378 | `VC_WFYCST` / `VC_WFYCST` | Gang | 0,077 | 0,080 | 984 | 724 | 0,016 | 1 / 1 | — | — |
| 48379 | `VC_WFYG1` / `VC_WFYG1` | Dân thường | 0,090 | 0,092 | 1.174 | 814 | 0,021 | 1 / 1 | Vice City | — |
| 48380 | `VC_WFYG2` / `VC_WFYG2` | Dân thường | 0,082 | 0,084 | 984 | 727 | 0,021 | 1 / 1 | Vice City | — |
| 48381 | `VC_WFYJG` / `VC_WFYJG` | Dân thường | 0,082 | 0,084 | 968 | 737 | 0,021 | 1 / 1 | Vice City | P1 |
| 48382 | `VC_WFYLG` / `VC_WFYLG` | Dân thường | 0,075 | 0,076 | 870 | 623 | 0,021 | 1 / 1 | Vice City | — |
| 48383 | `VC_WFYPR` / `VC_WFYPR` | Prostitute | 0,083 | 0,084 | 963 | 752 | 0,021 | 1 / 1 | — | — |
| 48384 | `VC_WFYRI` / `VC_WFYRI` | Dân thường | 0,085 | 0,086 | 929 | 809 | 0,021 | 1 / 1 | Vice City | P1 |
| 48385 | `VC_WFYSH` / `VC_WFYSH` | Dân thường | 0,084 | 0,088 | 980 | 880 | 0,016 | 1 / 1 | Vice City | — |
| 48386 | `VC_WFYSK` / `VC_WFYSK` | Dân thường | 0,086 | 0,088 | 997 | 808 | 0,021 | 1 / 1 | Vice City | — |
| 48387 | `VC_WFYST` / `VC_WFYST` | Dân thường | 0,098 | 0,100 | 1.142 | 988 | 0,021 | 1 / 1 | — | — |
| 48388 | `VC_WMOBE` / `VC_WMOBE` | Dân thường | 0,080 | 0,082 | 888 | 721 | 0,021 | 1 / 1 | Vice City | — |
| 48389 | `VC_WMOBU` / `VC_WMOBU` | Dân thường | 0,087 | 0,088 | 996 | 826 | 0,021 | 1 / 1 | Vice City | P1 |
| 48390 | `VC_WMOCA` / `VC_WMOCA` | Dân thường | 0,093 | 0,094 | 1.030 | 918 | 0,021 | 1 / 1 | Vice City | — |
| 48391 | `VC_WMOGO` / `VC_WMOGO` | Dân thường | 0,085 | 0,086 | 928 | 795 | 0,021 | 1 / 1 | — | — |
| 48392 | `VC_WMORI` / `VC_WMORI` | Dân thường | 0,082 | 0,084 | 996 | 826 | 0,016 | 1 / 1 | Vice City | P1 |
| 48393 | `VC_WMOST` / `VC_WMOST` | Dân thường | 0,105 | 0,105 | 1.065 | 1.146 | 0,021 | 1 / 1 | — | — |
| 48394 | `VC_WMOTR` / `VC_WMOTR` | Dân thường | 0,078 | 0,080 | 926 | 674 | 0,021 | 1 / 1 | Vice City | — |
| 48395 | `VC_WMYBE` / `VC_WMYBE` | Dân thường | 0,079 | 0,080 | 896 | 689 | 0,021 | 1 / 1 | Vice City | — |
| 48396 | `VC_WMYBU` / `VC_WMYBU` | Dân thường | 0,094 | 0,096 | 979 | 957 | 0,021 | 1 / 1 | Vice City | P1 |
| 48397 | `VC_WMYCR` / `VC_WMYCR` | Criminal | 0,091 | 0,094 | 988 | 999 | 0,016 | 1 / 1 | Vice City | — |
| 48398 | `VC_WMYCW` / `VC_WMYCW` | Dân thường | 0,078 | 0,080 | 916 | 667 | 0,021 | 1 / 1 | Vice City | — |
| 48399 | `VC_WMYGO` / `VC_WMYGO` | Dân thường | 0,092 | 0,094 | 966 | 930 | 0,021 | 1 / 1 | Vice City | — |
| 48400 | `VC_WMYJG` / `VC_WMYJG` | Dân thường | 0,077 | 0,078 | 904 | 662 | 0,021 | 1 / 1 | Vice City | — |
| 48401 | `VC_WMYLG` / `VC_WMYLG` | Dân thường | 0,077 | 0,078 | 876 | 659 | 0,021 | 1 / 1 | Vice City | — |
| 48402 | `VC_WMYPI` / `VC_WMYPI` | Criminal | 0,104 | 0,105 | 1.032 | 1.146 | 0,021 | 1 / 1 | Vice City | — |
| 48403 | `VC_WMYRI` / `VC_WMYRI` | Dân thường | 0,101 | 0,104 | 1.026 | 1.099 | 0,021 | 1 / 1 | Vice City | P1 |
| 48404 | `VC_WMYSK` / `VC_WMYSK` | Dân thường | 0,093 | 0,094 | 1.070 | 916 | 0,021 | 1 / 1 | Vice City | — |
| 48405 | `VC_WMYST` / `VC_WMYST` | Dân thường | 0,105 | 0,107 | 1.094 | 1.146 | 0,021 | 1 / 1 | Vice City | — |
| 48406 | `LC_8BALL` / `LC_8BALL` | Gang | 0,302 | 0,305 | 2.305 | 1.550 | 0,174 | 2 / 3 | — | — |
| 48407 | `LC_8BALLPRISON` / `LC_8BALLPRISON` | Gang | 0,306 | 0,309 | 2.269 | 1.649 | 0,174 | 2 / 2 | — | — |
| 48408 | `LC_AM` / `LC_AM` | Dân thường | 0,078 | 0,080 | 1.026 | 879 | 0,008 | 1 / 3 | — | — |
| 48409 | `LC_ARMY` / `LC_ARMY` | Cảnh sát / quân đội / cứu hộ | 0,113 | 0,115 | 1.590 | 1.378 | 0,008 | 1 / 1 | — | — |
| 48410 | `LC_ASUKA` / `LC_ASUKA` | Dân thường | 0,347 | 0,350 | 3.234 | 2.258 | 0,167 | 1 / 1 | — | — |
| 48411 | `LC_B_MAN1` / `LC_B_MAN1` | Dân thường | 0,132 | 0,135 | 1.184 | 1.916 | 0,008 | 1 / 1 | — | — |
| 48412 | `LC_B_MAN2` / `LC_B_MAN2` | Dân thường | 0,141 | 0,145 | 1.398 | 2.018 | 0,008 | 1 / 1 | — | — |
| 48413 | `LC_B_MAN3` / `LC_B_MAN3` | Dân thường | 0,071 | 0,074 | 892 | 793 | 0,008 | 1 / 1 | — | — |
| 48414 | `LC_B_WOM1` / `LC_B_WOM1` | Dân thường | 0,070 | 0,072 | 968 | 747 | 0,008 | 1 / 1 | — | — |
| 48415 | `LC_B_WOM2` / `LC_B_WOM2` | Dân thường | 0,133 | 0,137 | 1.239 | 1.924 | 0,008 | 1 / 1 | — | — |
| 48416 | `LC_B_WOM3` / `LC_B_WOM3` | Dân thường | 0,134 | 0,137 | 1.277 | 1.916 | 0,008 | 1 / 1 | — | — |
| 48417 | `LC_BOMBER` / `LC_BOMBER` | Dân thường | 0,152 | 0,154 | 1.515 | 2.187 | 0,008 | 1 / 3 | — | — |
| 48418 | `LC_CABBIEDRV` / `LC_CABBIEDRV` | Dân thường | 0,060 | 0,062 | 668 | 664 | 0,008 | 1 / 1 | — | — |
| 48419 | `LC_CAS_MAN` / `LC_CAS_MAN` | Dân thường | 0,105 | 0,107 | 1.614 | 1.207 | 0,008 | 1 / 3 | — | — |
| 48420 | `LC_CAS_WOM` / `LC_CAS_WOM` | Dân thường | 0,086 | 0,090 | 1.076 | 1.034 | 0,008 | 1 / 1 | — | — |
| 48421 | `LC_CAT` / `LC_CAT` | Dân thường | 0,411 | 0,412 | 3.799 | 3.117 | 0,177 | 2 / 4 | — | — |
| 48422 | `LC_CHUNKY` / `LC_CHUNKY` | Dân thường | 0,071 | 0,074 | 870 | 799 | 0,008 | 1 / 4 | — | — |
| 48423 | `LC_CLAUDE` / `LC_CLAUDE` | Model có pedtype PLAYER1/2 | 0,332 | 0,334 | 2.937 | 2.076 | 0,167 | 1 / 1 | — | — |
| 48424 | `LC_CLAUDE2` / `LC_CLAUDE2` | Model có pedtype PLAYER1/2 | 0,329 | 0,332 | 2.901 | 2.030 | 0,167 | 1 / 1 | — | — |
| 48425 | `LC_CLAUDEPRISON` / `LC_CLAUDEPRISON` | Model có pedtype PLAYER1/2 | 0,325 | 0,328 | 2.863 | 1.964 | 0,167 | 1 / 1 | — | — |
| 48426 | `LC_COL1` / `LC_COL1` | Dân thường | 0,102 | 0,105 | 1.269 | 1.282 | 0,008 | 1 / 2 | — | — |
| 48427 | `LC_COL2` / `LC_COL2` | Dân thường | 0,106 | 0,107 | 1.361 | 1.317 | 0,008 | 1 / 1 | — | — |
| 48428 | `LC_COL3` / `LC_COL3` | Dân thường | 0,121 | 0,123 | 1.479 | 1.580 | 0,008 | 1 / 1 | — | — |
| 48429 | `LC_COLROB` / `LC_COLROB` | Dân thường | 0,117 | 0,119 | 1.798 | 1.369 | 0,008 | 1 / 1 | — | — |
| 48430 | `LC_CONST1` / `LC_CONST1` | Dân thường | 0,087 | 0,090 | 1.021 | 1.060 | 0,008 | 1 / 4 | — | — |
| 48431 | `LC_CONST2` / `LC_CONST2` | Dân thường | 0,087 | 0,090 | 1.021 | 1.060 | 0,008 | 1 / 4 | — | — |
| 48432 | `LC_COP` / `LC_COP` | Cảnh sát / quân đội / cứu hộ | 0,113 | 0,115 | 1.478 | 1.417 | 0,008 | 1 / 2 | — | — |
| 48433 | `LC_CRIMINAL01` / `LC_CRIMINAL01` | Criminal | 0,133 | 0,135 | 1.678 | 1.732 | 0,008 | 1 / 4 | — | — |
| 48434 | `LC_CRIMINAL02` / `LC_CRIMINAL02` | Criminal | 0,158 | 0,160 | 1.878 | 2.170 | 0,008 | 1 / 4 | — | — |
| 48435 | `LC_CT_MAN1` / `LC_CT_MAN1` | Dân thường | 0,071 | 0,074 | 911 | 733 | 0,010 | 1 / 4 | — | — |
| 48436 | `LC_CT_MAN2` / `LC_CT_MAN2` | Dân thường | 0,113 | 0,115 | 1.460 | 1.355 | 0,010 | 1 / 4 | — | — |
| 48437 | `LC_CT_WOM1` / `LC_CT_WOM1` | Dân thường | 0,076 | 0,078 | 908 | 833 | 0,010 | 1 / 3 | — | — |
| 48438 | `LC_CT_WOM2` / `LC_CT_WOM2` | Dân thường | 0,070 | 0,072 | 782 | 750 | 0,010 | 1 / 4 | — | — |
| 48439 | `LC_CURLY` / `LC_CURLY` | Dân thường | 0,562 | 0,564 | 4.248 | 5.999 | 0,177 | 2 / 2 | — | — |
| 48440 | `LC_DEALER` / `LC_DEALER` | Dân thường | 0,066 | 0,068 | 801 | 667 | 0,010 | 1 / 3 | — | — |
| 48441 | `LC_DOCKER1` / `LC_DOCKER1` | Dân thường | 0,094 | 0,096 | 1.218 | 1.094 | 0,010 | 1 / 1 | — | — |
| 48442 | `LC_DOCKER2` / `LC_DOCKER2` | Dân thường | 0,067 | 0,068 | 730 | 718 | 0,010 | 1 / 4 | — | — |
| 48443 | `LC_FAN_MAN1` / `LC_FAN_MAN1` | Dân thường | 0,099 | 0,102 | 1.304 | 1.148 | 0,010 | 1 / 4 | — | — |
| 48444 | `LC_FAN_MAN2` / `LC_FAN_MAN2` | Dân thường | 0,068 | 0,070 | 804 | 704 | 0,010 | 1 / 4 | — | — |
| 48445 | `LC_FAN_WOM` / `LC_FAN_WOM` | Dân thường | 0,107 | 0,109 | 1.089 | 1.386 | 0,010 | 1 / 4 | — | — |
| 48446 | `LC_FATFEMALE01` / `LC_FATFEMALE01` | Dân thường | 0,071 | 0,074 | 913 | 740 | 0,010 | 1 / 2 | — | — |
| 48447 | `LC_FATFEMALE02` / `LC_FATFEMALE02` | Dân thường | 0,075 | 0,078 | 919 | 816 | 0,010 | 1 / 2 | — | — |
| 48448 | `LC_FATMALE01` / `LC_FATMALE01` | Dân thường | 0,076 | 0,078 | 900 | 842 | 0,010 | 1 / 1 | — | — |
| 48449 | `LC_FATMALE02` / `LC_FATMALE02` | Dân thường | 0,066 | 0,068 | 846 | 660 | 0,010 | 1 / 4 | — | — |
| 48450 | `LC_FBI` / `LC_FBI` | Cảnh sát / quân đội / cứu hộ | 0,127 | 0,129 | 1.684 | 1.458 | 0,016 | 1 / 4 | — | — |
| 48451 | `LC_FEMALE01` / `LC_FEMALE01` | Dân thường | 0,104 | 0,105 | 960 | 1.367 | 0,010 | 1 / 4 | — | — |
| 48452 | `LC_FEMALE02` / `LC_FEMALE02` | Dân thường | 0,075 | 0,076 | 920 | 806 | 0,010 | 1 / 4 | — | — |
| 48453 | `LC_FEMALE03` / `LC_FEMALE03` | Dân thường | 0,076 | 0,078 | 860 | 841 | 0,010 | 1 / 4 | — | — |
| 48454 | `LC_FIREMAN` / `LC_FIREMAN` | Cảnh sát / quân đội / cứu hộ | 0,175 | 0,178 | 1.533 | 2.656 | 0,008 | 1 / 2 | — | — |
| 48455 | `LC_G_COLUMB01` / `LC_G_COLUMB01` | Gang | 0,146 | 0,148 | 1.473 | 2.095 | 0,008 | 1 / 2 | — | — |
| 48456 | `LC_G_COLUMB02` / `LC_G_COLUMB02` | Gang | 0,146 | 0,148 | 1.473 | 2.095 | 0,008 | 1 / 2 | — | — |
| 48457 | `LC_G_DIABLO01` / `LC_G_DIABLO01` | Gang | 0,117 | 0,119 | 1.451 | 1.515 | 0,008 | 1 / 1 | — | — |
| 48458 | `LC_G_DIABLO02` / `LC_G_DIABLO02` | Gang | 0,117 | 0,119 | 1.451 | 1.515 | 0,008 | 1 / 1 | — | — |
| 48459 | `LC_G_LEONE01` / `LC_G_LEONE01` | Gang | 0,139 | 0,143 | 1.452 | 1.965 | 0,008 | 1 / 1 | — | — |
| 48460 | `LC_G_LEONE02` / `LC_G_LEONE02` | Gang | 0,459 | 0,461 | 1.608 | 2.198 | 0,312 | 2 / 1 | — | — |
| 48461 | `LC_G_TRIAD01` / `LC_G_TRIAD01` | Gang | 0,075 | 0,078 | 950 | 861 | 0,008 | 1 / 2 | — | — |
| 48462 | `LC_G_TRIAD02` / `LC_G_TRIAD02` | Gang | 0,083 | 0,086 | 950 | 861 | 0,016 | 1 / 2 | — | — |
| 48463 | `LC_G_YAKUZA01` / `LC_G_YAKUZA01` | Gang | 0,152 | 0,154 | 1.374 | 2.256 | 0,008 | 1 / 1 | — | — |
| 48464 | `LC_G_YAKUZA02` / `LC_G_YAKUZA02` | Gang | 0,152 | 0,154 | 1.374 | 2.256 | 0,008 | 1 / 1 | — | — |
| 48465 | `LC_G_YARDIE01` / `LC_G_YARDIE01` | Gang | 0,195 | 0,197 | 1.844 | 2.930 | 0,008 | 1 / 4 | — | — |
| 48466 | `LC_G_YARDIE02` / `LC_G_YARDIE02` | Gang | 0,195 | 0,197 | 1.844 | 2.930 | 0,008 | 1 / 4 | — | — |
| 48467 | `LC_GOON` / `LC_GOON` | Gang | 0,065 | 0,068 | 858 | 637 | 0,010 | 1 / 4 | — | — |
| 48468 | `LC_HOODS01` / `LC_HOODS01` | Gang | 0,098 | 0,100 | 1.365 | 1.115 | 0,010 | 1 / 1 | — | — |
| 48469 | `LC_HOODS02` / `LC_HOODS02` | Gang | 0,098 | 0,100 | 1.365 | 1.115 | 0,010 | 1 / 1 | — | — |
| 48470 | `LC_HOS_MAN` / `LC_HOS_MAN` | Cảnh sát / quân đội / cứu hộ | 0,072 | 0,074 | 860 | 773 | 0,010 | 1 / 4 | — | — |
| 48471 | `LC_HOS_WOM` / `LC_HOS_WOM` | Cảnh sát / quân đội / cứu hộ | 0,068 | 0,070 | 782 | 717 | 0,010 | 1 / 4 | — | — |
| 48472 | `LC_JOEY` / `LC_JOEY` | Gang | 0,355 | 0,357 | 3.316 | 2.179 | 0,177 | 2 / 2 | — | — |
| 48473 | `LC_JOEY2` / `LC_JOEY2` | Gang | 0,345 | 0,346 | 2.989 | 2.105 | 0,177 | 2 / 2 | — | — |
| 48474 | `LC_KEEPER` / `LC_KEEPER` | Dân thường | 0,082 | 0,084 | 794 | 996 | 0,010 | 1 / 4 | — | — |
| 48475 | `LC_KENJI` / `LC_KENJI` | Dân thường | 0,456 | 0,457 | 3.829 | 4.015 | 0,177 | 2 / 2 | — | — |
| 48476 | `LC_LI_MAN1` / `LC_LI_MAN1` | Dân thường | 0,074 | 0,076 | 894 | 787 | 0,010 | 1 / 4 | — | — |
| 48477 | `LC_LI_MAN2` / `LC_LI_MAN2` | Dân thường | 0,113 | 0,115 | 1.390 | 1.385 | 0,010 | 1 / 4 | — | — |
| 48478 | `LC_LI_WOM1` / `LC_LI_WOM1` | Dân thường | 0,076 | 0,078 | 908 | 833 | 0,010 | 1 / 3 | — | — |
| 48479 | `LC_LI_WOM2` / `LC_LI_WOM2` | Dân thường | 0,080 | 0,082 | 927 | 900 | 0,010 | 1 / 4 | — | — |
| 48480 | `LC_LIPS` / `LC_LIPS` | Dân thường | 0,080 | 0,082 | 956 | 902 | 0,010 | 1 / 4 | — | — |
| 48481 | `LC_LOVE` / `LC_LOVE` | Dân thường | 0,451 | 0,451 | 3.218 | 4.136 | 0,177 | 2 / 3 | — | — |
| 48482 | `LC_LOVE2` / `LC_LOVE2` | Dân thường | 0,362 | 0,363 | 3.486 | 2.244 | 0,177 | 2 / 2 | — | — |
| 48483 | `LC_LUIGI` / `LC_LUIGI` | Gang | 0,359 | 0,359 | 3.274 | 2.263 | 0,177 | 2 / 2 | — | — |
| 48484 | `LC_MALE01` / `LC_MALE01` | Dân thường | 0,076 | 0,078 | 937 | 866 | 0,008 | 1 / 3 | — | — |
| 48485 | `LC_MALE02` / `LC_MALE02` | Dân thường | 0,161 | 0,162 | 1.200 | 1.602 | 0,052 | 2 / 3 | — | — |
| 48486 | `LC_MALE03` / `LC_MALE03` | Dân thường | 0,132 | 0,135 | 1.217 | 1.895 | 0,008 | 1 / 1 | — | — |
| 48487 | `LC_MEDIC` / `LC_MEDIC` | Cảnh sát / quân đội / cứu hộ | 0,079 | 0,082 | 1.027 | 917 | 0,008 | 1 / 1 | — | — |
| 48488 | `LC_MICKY` / `LC_MICKY` | Gang | 0,357 | 0,359 | 3.293 | 2.227 | 0,177 | 2 / 3 | — | — |
| 48489 | `LC_MIGUEL` / `LC_MIGUEL` | Dân thường | 0,363 | 0,365 | 3.354 | 2.320 | 0,177 | 2 / 2 | — | — |
| 48490 | `LC_MISTY` / `LC_MISTY` | Prostitute | 0,375 | 0,375 | 3.523 | 2.491 | 0,177 | 2 / 2 | — | — |
| 48491 | `LC_MOD_MAN` / `LC_MOD_MAN` | Dân thường | 0,132 | 0,135 | 1.184 | 1.916 | 0,008 | 1 / 1 | — | — |
| 48492 | `LC_MOD_WOM` / `LC_MOD_WOM` | Dân thường | 0,095 | 0,098 | 978 | 1.244 | 0,008 | 1 / 4 | — | — |
| 48493 | `LC_OJG` / `LC_OJG` | Dân thường | 0,217 | 0,219 | 2.849 | 2.100 | 0,052 | 2 / 2 | — | — |
| 48494 | `LC_OJG_P` / `LC_OJG_P` | Dân thường | 0,370 | 0,371 | 3.346 | 2.459 | 0,177 | 2 / 2 | — | — |
| 48495 | `LC_OJG2` / `LC_OJG2` | Dân thường | 0,320 | 0,320 | 3.644 | 3.858 | 0,052 | 2 / 2 | — | — |
| 48496 | `LC_P_MAN1` / `LC_P_MAN1` | Dân thường | 0,097 | 0,100 | 1.026 | 1.213 | 0,010 | 1 / 4 | — | — |
| 48497 | `LC_P_MAN2` / `LC_P_MAN2` | Dân thường | 0,077 | 0,080 | 930 | 847 | 0,010 | 1 / 4 | — | — |
| 48498 | `LC_P_WOM1` / `LC_P_WOM1` | Dân thường | 0,076 | 0,078 | 908 | 833 | 0,010 | 1 / 3 | — | — |
| 48499 | `LC_P_WOM2` / `LC_P_WOM2` | Dân thường | 0,079 | 0,082 | 927 | 900 | 0,010 | 1 / 1 | — | — |
| 48500 | `LC_PIMP` / `LC_PIMP` | Dân thường | 0,099 | 0,102 | 1.332 | 1.140 | 0,010 | 1 / 4 | — | — |
| 48501 | `LC_PROSTITUTE` / `LC_PROSTITUTE` | Prostitute | 0,069 | 0,072 | 841 | 759 | 0,008 | 1 / 4 | — | — |
| 48502 | `LC_PROSTITUTE02` / `LC_PROSTITUTE02` | Prostitute | 0,108 | 0,111 | 1.471 | 1.312 | 0,008 | 1 / 2 | — | — |
| 48503 | `LC_RAY` / `LC_RAY` | Cảnh sát / quân đội / cứu hộ | 0,433 | 0,434 | 3.367 | 3.721 | 0,177 | 2 / 3 | — | — |
| 48504 | `LC_ROBBER` / `LC_ROBBER` | Gang | 0,101 | 0,104 | 936 | 1.319 | 0,010 | 1 / 4 | — | — |
| 48505 | `LC_S_GUARD` / `LC_S_GUARD` | Dân thường | 0,148 | 0,150 | 2.008 | 1.861 | 0,010 | 1 / 1 | — | — |
| 48506 | `LC_SALVATORE` / `LC_SALVATORE` | Gang | 0,478 | 0,479 | 3.588 | 4.540 | 0,177 | 2 / 3 | — | — |
| 48507 | `LC_SCUM_MAN` / `LC_SCUM_MAN` | Dân thường | 0,087 | 0,088 | 1.055 | 997 | 0,010 | 1 / 1 | — | — |
| 48508 | `LC_SCUM_WOM` / `LC_SCUM_WOM` | Dân thường | 0,091 | 0,094 | 1.161 | 1.047 | 0,010 | 1 / 3 | — | — |
| 48509 | `LC_SHOPPER01` / `LC_SHOPPER01` | Dân thường | 0,068 | 0,070 | 800 | 784 | 0,008 | 1 / 1 | — | — |
| 48510 | `LC_SHOPPER02` / `LC_SHOPPER02` | Dân thường | 0,073 | 0,076 | 920 | 819 | 0,008 | 1 / 3 | — | — |
| 48511 | `LC_SHOPPER03` / `LC_SHOPPER03` | Dân thường | 0,095 | 0,098 | 1.232 | 1.148 | 0,008 | 1 / 4 | — | — |
| 48512 | `LC_ST_MAN` / `LC_ST_MAN` | Dân thường | 0,070 | 0,072 | 833 | 802 | 0,008 | 1 / 1 | — | — |
| 48513 | `LC_ST_WOM` / `LC_ST_WOM` | Dân thường | 0,082 | 0,084 | 986 | 929 | 0,010 | 1 / 2 | — | — |
| 48514 | `LC_STUD_MAN` / `LC_STUD_MAN` | Gang | 0,065 | 0,066 | 730 | 668 | 0,010 | 1 / 4 | — | — |
| 48515 | `LC_STUD_WOM` / `LC_STUD_WOM` | Gang | 0,099 | 0,102 | 951 | 1.276 | 0,010 | 1 / 4 | — | — |
| 48516 | `LC_SWAT` / `LC_SWAT` | Cảnh sát / quân đội / cứu hộ | 0,088 | 0,092 | 1.082 | 1.075 | 0,008 | 1 / 1 | — | — |
| 48517 | `LC_TANNER` / `LC_TANNER` | Cảnh sát / quân đội / cứu hộ | 0,086 | 0,088 | 958 | 1.074 | 0,008 | 1 / 1 | — | — |
| 48518 | `LC_TONY` / `LC_TONY` | Gang | 0,530 | 0,531 | 4.060 | 5.410 | 0,177 | 2 / 2 | — | — |
| 48519 | `LC_WORKER1` / `LC_WORKER1` | Dân thường | 0,069 | 0,070 | 846 | 710 | 0,010 | 1 / 4 | — | — |
| 48520 | `LC_WORKER2` / `LC_WORKER2` | Dân thường | 0,073 | 0,076 | 917 | 770 | 0,010 | 1 / 4 | — | — |
| 48521 | `CC_BUNNY` / `CC_BUNNY` | Dân thường | 0,165 | 0,166 | 1.329 | 998 | 0,083 | 2 / 2 | — | — |
| 48522 | `CC_CASH` / `CC_CASH` | Model có pedtype PLAYER1/2 | 0,208 | 0,211 | 2.176 | 1.961 | 0,062 | 2 / 2 | — | — |
| 48523 | `CC_CCPD1` / `CC_CCPD1` | Cảnh sát / quân đội / cứu hộ | 0,179 | 0,180 | 1.382 | 1.265 | 0,083 | 2 / 2 | — | — |
| 48524 | `CC_CCPD2` / `CC_CCPD2` | Cảnh sát / quân đội / cứu hộ | 0,179 | 0,180 | 1.382 | 1.265 | 0,083 | 2 / 2 | — | — |
| 48525 | `CC_CCPD3` / `CC_CCPD3` | Cảnh sát / quân đội / cứu hộ | 0,179 | 0,180 | 1.382 | 1.265 | 0,083 | 2 / 2 | — | — |
| 48526 | `CC_CCPD4` / `CC_CCPD4` | Cảnh sát / quân đội / cứu hộ | 0,173 | 0,174 | 1.312 | 1.173 | 0,083 | 2 / 2 | — | — |
| 48527 | `CC_CCPD5` / `CC_CCPD5` | Cảnh sát / quân đội / cứu hộ | 0,173 | 0,174 | 1.312 | 1.173 | 0,083 | 2 / 2 | — | — |
| 48528 | `CC_CCPD6` / `CC_CCPD6` | Cảnh sát / quân đội / cứu hộ | 0,173 | 0,174 | 1.312 | 1.173 | 0,083 | 2 / 2 | — | — |
| 48529 | `CC_CERBEROUS1` / `CC_CERBEROUS1` | Gang | 0,193 | 0,195 | 1.316 | 1.569 | 0,083 | 2 / 2 | Carcer City | — |
| 48530 | `CC_CERBEROUS2` / `CC_CERBEROUS2` | Gang | 0,193 | 0,195 | 1.316 | 1.569 | 0,083 | 2 / 2 | Carcer City | — |
| 48531 | `CC_CERBEROUS3` / `CC_CERBEROUS3` | Gang | 0,193 | 0,195 | 1.316 | 1.569 | 0,083 | 2 / 2 | Carcer City | — |
| 48532 | `CC_CERBEROUS4` / `CC_CERBEROUS4` | Gang | 0,218 | 0,219 | 1.728 | 1.905 | 0,083 | 2 / 2 | Carcer City | — |
| 48533 | `CC_HOOD1` / `CC_HOOD1` | Gang | 0,180 | 0,182 | 1.351 | 1.279 | 0,083 | 2 / 2 | — | — |
| 48534 | `CC_HOOD2` / `CC_HOOD2` | Gang | 0,180 | 0,182 | 1.351 | 1.279 | 0,083 | 2 / 2 | — | — |
| 48535 | `CC_HOOD3` / `CC_HOOD3` | Gang | 0,180 | 0,182 | 1.351 | 1.279 | 0,083 | 2 / 2 | — | — |
| 48536 | `CC_HOOD4` / `CC_HOOD4` | Gang | 0,175 | 0,176 | 1.294 | 1.213 | 0,083 | 2 / 2 | — | — |
| 48537 | `CC_HOOD5` / `CC_HOOD5` | Gang | 0,175 | 0,176 | 1.294 | 1.213 | 0,083 | 2 / 2 | — | — |
| 48538 | `CC_HOOD6` / `CC_HOOD6` | Gang | 0,175 | 0,176 | 1.294 | 1.213 | 0,083 | 2 / 2 | — | — |
| 48539 | `CC_HOOD7` / `CC_HOOD7` | Gang | 0,186 | 0,188 | 1.380 | 1.404 | 0,083 | 2 / 2 | — | — |
| 48540 | `CC_HOOD8` / `CC_HOOD8` | Gang | 0,186 | 0,188 | 1.380 | 1.404 | 0,083 | 2 / 2 | — | — |
| 48541 | `CC_HOOD9` / `CC_HOOD9` | Gang | 0,186 | 0,188 | 1.380 | 1.404 | 0,083 | 2 / 2 | — | — |
| 48542 | `CC_HOSTAGE1` / `CC_HOSTAGE1` | Dân thường | 0,161 | 0,162 | 1.290 | 927 | 0,083 | 2 / 2 | — | — |
| 48543 | `CC_HOSTAGE2` / `CC_HOSTAGE2` | Dân thường | 0,169 | 0,170 | 1.369 | 1.052 | 0,083 | 2 / 2 | — | — |
| 48544 | `CC_HOSTAGE3` / `CC_HOSTAGE3` | Dân thường | 0,161 | 0,162 | 1.290 | 927 | 0,083 | 2 / 2 | — | — |
| 48545 | `CC_HOSTAGE4` / `CC_HOSTAGE4` | Dân thường | 0,169 | 0,170 | 1.369 | 1.052 | 0,083 | 2 / 2 | — | — |
| 48546 | `CC_INOCENTZ1` / `CC_INOCENTZ1` | Gang | 0,171 | 0,172 | 1.280 | 1.140 | 0,083 | 2 / 2 | — | — |
| 48547 | `CC_INOCENTZ2` / `CC_INOCENTZ2` | Gang | 0,171 | 0,172 | 1.280 | 1.140 | 0,083 | 2 / 2 | — | — |
| 48548 | `CC_INOCENTZ3` / `CC_INOCENTZ3` | Gang | 0,171 | 0,172 | 1.280 | 1.140 | 0,083 | 2 / 2 | — | — |
| 48549 | `CC_INOCENTZ4` / `CC_INOCENTZ4` | Gang | 0,155 | 0,156 | 1.399 | 1.396 | 0,052 | 2 / 2 | — | — |
| 48550 | `CC_INOCENTZ5` / `CC_INOCENTZ5` | Gang | 0,186 | 0,188 | 1.399 | 1.396 | 0,083 | 2 / 2 | — | — |
| 48551 | `CC_INOCENTZ6` / `CC_INOCENTZ6` | Gang | 0,155 | 0,156 | 1.399 | 1.396 | 0,052 | 2 / 2 | — | — |
| 48552 | `CC_INOCENTZ7` / `CC_INOCENTZ7` | Gang | 0,181 | 0,182 | 1.356 | 1.312 | 0,083 | 2 / 2 | — | — |
| 48553 | `CC_INOCENTZ8` / `CC_INOCENTZ8` | Gang | 0,181 | 0,182 | 1.356 | 1.312 | 0,083 | 2 / 2 | — | — |
| 48554 | `CC_INOCENTZ9` / `CC_INOCENTZ9` | Gang | 0,181 | 0,182 | 1.356 | 1.312 | 0,083 | 2 / 2 | — | — |
| 48555 | `CC_JOURNALIST` / `CC_JOURNALIST` | Dân thường | 0,128 | 0,129 | 1.609 | 1.395 | 0,021 | 2 / 2 | — | — |
| 48556 | `CC_MONKEY` / `CC_MONKEY` | Dân thường | 0,200 | 0,201 | 1.802 | 1.519 | 0,083 | 2 / 2 | — | — |
| 48557 | `CC_PIGGSY` / `CC_PIGGSY` | Dân thường | 0,226 | 0,229 | 2.374 | 2.247 | 0,063 | 2 / 2 | — | — |
| 48558 | `CC_RAMIREZ` / `CC_RAMIREZ` | Dân thường | 0,176 | 0,178 | 1.423 | 1.176 | 0,083 | 2 / 2 | — | — |
| 48559 | `CC_SKINZ1` / `CC_SKINZ1` | Gang | 0,149 | 0,152 | 1.282 | 1.120 | 0,062 | 2 / 2 | — | — |
| 48560 | `CC_SKINZ2` / `CC_SKINZ2` | Gang | 0,170 | 0,172 | 1.282 | 1.120 | 0,083 | 2 / 2 | — | — |
| 48561 | `CC_SKINZ3` / `CC_SKINZ3` | Gang | 0,170 | 0,172 | 1.282 | 1.120 | 0,083 | 2 / 2 | — | — |
| 48562 | `CC_SKINZ4` / `CC_SKINZ4` | Gang | 0,151 | 0,154 | 1.334 | 1.132 | 0,062 | 2 / 2 | — | — |
| 48563 | `CC_SKINZ5` / `CC_SKINZ5` | Gang | 0,172 | 0,174 | 1.334 | 1.132 | 0,083 | 2 / 2 | — | — |
| 48564 | `CC_SKINZ6` / `CC_SKINZ6` | Gang | 0,172 | 0,174 | 1.334 | 1.132 | 0,083 | 2 / 2 | — | — |
| 48565 | `CC_SKINZ7` / `CC_SKINZ7` | Gang | 0,154 | 0,156 | 1.362 | 1.188 | 0,062 | 2 / 2 | — | — |
| 48566 | `CC_SKINZ8` / `CC_SKINZ8` | Gang | 0,175 | 0,176 | 1.362 | 1.188 | 0,083 | 2 / 2 | — | — |
| 48567 | `CC_SKINZ9` / `CC_SKINZ9` | Gang | 0,175 | 0,176 | 1.362 | 1.188 | 0,083 | 2 / 2 | — | — |
| 48568 | `CC_SMILEY1` / `CC_SMILEY1` | Gang | 0,179 | 0,180 | 1.377 | 1.264 | 0,083 | 2 / 2 | Carcer City | — |
| 48569 | `CC_SMILEY2` / `CC_SMILEY2` | Gang | 0,179 | 0,180 | 1.377 | 1.264 | 0,083 | 2 / 2 | Carcer City | — |
| 48570 | `CC_SMILEY3` / `CC_SMILEY3` | Gang | 0,179 | 0,180 | 1.377 | 1.264 | 0,083 | 2 / 2 | Carcer City | — |
| 48571 | `CC_SMILEY4` / `CC_SMILEY4` | Gang | 0,177 | 0,178 | 1.356 | 1.226 | 0,083 | 2 / 2 | Carcer City | — |
| 48572 | `CC_SMILEY5` / `CC_SMILEY5` | Gang | 0,177 | 0,178 | 1.356 | 1.226 | 0,083 | 2 / 2 | Carcer City | — |
| 48573 | `CC_SMILEY6` / `CC_SMILEY6` | Gang | 0,177 | 0,178 | 1.356 | 1.226 | 0,083 | 2 / 2 | Carcer City | — |
| 48574 | `CC_SMILEY7` / `CC_SMILEY7` | Gang | 0,156 | 0,158 | 1.363 | 1.212 | 0,062 | 2 / 2 | Carcer City | — |
| 48575 | `CC_SMILEY8` / `CC_SMILEY8` | Gang | 0,176 | 0,178 | 1.363 | 1.212 | 0,083 | 2 / 2 | Carcer City | — |
| 48576 | `CC_SMILEY9` / `CC_SMILEY9` | Gang | 0,176 | 0,178 | 1.363 | 1.212 | 0,083 | 2 / 2 | Carcer City | — |
| 48577 | `CC_STARKWEATHER` / `CC_STARKWEATHER` | Dân thường | 0,209 | 0,209 | 1.861 | 1.670 | 0,083 | 2 / 2 | — | — |
| 48578 | `CC_SWAT` / `CC_SWAT` | Cảnh sát / quân đội / cứu hộ | 0,176 | 0,178 | 1.306 | 1.227 | 0,083 | 2 / 2 | — | — |
| 48579 | `CC_TRMP` / `CC_TRMP` | Dân thường | 0,185 | 0,188 | 1.279 | 1.426 | 0,083 | 2 / 2 | — | — |
| 48580 | `CC_TRUMP` / `CC_TRUMP` | Dân thường | 0,164 | 0,168 | 1.279 | 1.426 | 0,062 | 2 / 2 | — | — |
| 48581 | `CC_WARDOG1` / `CC_WARDOG1` | Gang | 0,178 | 0,180 | 1.307 | 1.256 | 0,083 | 2 / 2 | — | — |
| 48582 | `CC_WARDOG2` / `CC_WARDOG2` | Gang | 0,191 | 0,191 | 1.396 | 1.489 | 0,083 | 2 / 2 | — | — |
| 48583 | `CC_WARDOG3` / `CC_WARDOG3` | Gang | 0,191 | 0,191 | 1.396 | 1.489 | 0,083 | 2 / 2 | — | — |
| 48584 | `CC_WARDOG4` / `CC_WARDOG4` | Gang | 0,191 | 0,191 | 1.396 | 1.489 | 0,083 | 2 / 2 | — | — |
| 48585 | `CC_WARDOG5` / `CC_WARDOG5` | Gang | 0,231 | 0,232 | 1.651 | 2.199 | 0,083 | 2 / 2 | — | — |
| 48586 | `CC_WARDOG6` / `CC_WARDOG6` | Gang | 0,178 | 0,180 | 1.307 | 1.256 | 0,083 | 2 / 2 | — | — |
| 48587 | `CC_WARDOG7` / `CC_WARDOG7` | Gang | 0,178 | 0,180 | 1.307 | 1.256 | 0,083 | 2 / 2 | — | — |
| 48588 | `CC_WARDOG8` / `CC_WARDOG8` | Gang | 0,231 | 0,232 | 1.651 | 2.199 | 0,083 | 2 / 2 | — | — |
| 48589 | `CC_ZOMBIE` / `CC_ZOMBIE` | Dân thường | 0,162 | 0,162 | 1.820 | 1.370 | 0,052 | 2 / 3 | — | — |
| 48590 | `BW_ABOWNER` / `BW_ABOWNER` | Dân thường | 0,465 | 0,467 | 1.868 | 1.788 | 0,333 | 2 / 4 | — | — |
| 48591 | `BW_AS_HENRY` / `BW_AS_HENRY` | Cảnh sát / quân đội / cứu hộ | 0,446 | 0,447 | 1.815 | 1.437 | 0,333 | 2 / 2 | — | — |
| 48592 | `BW_AS_JONATHAN` / `BW_AS_JONATHAN` | Cảnh sát / quân đội / cứu hộ | 0,414 | 0,416 | 1.226 | 1.031 | 0,333 | 1 / 1 | — | — |
| 48593 | `BW_AS_LEON` / `BW_AS_LEON` | Cảnh sát / quân đội / cứu hộ | 0,426 | 0,428 | 1.484 | 1.167 | 0,333 | 2 / 2 | — | — |
| 48594 | `BW_AS_OTTO` / `BW_AS_OTTO` | Cảnh sát / quân đội / cứu hộ | 0,482 | 0,484 | 1.674 | 1.356 | 0,375 | 3 / 4 | — | — |
| 48595 | `BW_AS_THEO` / `BW_AS_THEO` | Cảnh sát / quân đội / cứu hộ | 0,427 | 0,428 | 1.380 | 1.213 | 0,333 | 2 / 2 | — | — |
| 48596 | `BW_AS_WMYASY1` / `BW_AS_WMYASY1` | Dân thường | 0,465 | 0,467 | 1.521 | 1.947 | 0,333 | 1 / 1 | — | — |
| 48597 | `BW_BARBER_P` / `BW_BARBER_P` | Dân thường | 0,434 | 0,436 | 1.316 | 1.169 | 0,344 | 3 / 3 | — | — |
| 48598 | `BW_BARBER_R` / `BW_BARBER_R` | Dân thường | 0,437 | 0,439 | 1.646 | 1.326 | 0,333 | 2 / 2 | — | — |
| 48599 | `BW_BEARDEDWOMAN` / `BW_BEARDEDWOMAN` | Dân thường | 0,435 | 0,436 | 1.583 | 1.294 | 0,333 | 2 / 3 | — | — |
| 48600 | `BW_BIKEOWNER` / `BW_BIKEOWNER` | Dân thường | 0,426 | 0,428 | 1.430 | 1.191 | 0,333 | 1 / 1 | — | — |
| 48601 | `BW_BL_DAVIS` / `BW_BL_DAVIS` | Gang | 0,423 | 0,424 | 1.470 | 1.117 | 0,333 | 1 / 1 | — | — |
| 48602 | `BW_BL_ETHAN` / `BW_BL_ETHAN` | Gang | 0,448 | 0,449 | 1.826 | 1.487 | 0,333 | 1 / 1 | — | — |
| 48603 | `BW_BL_RUSSEL` / `BW_BL_RUSSEL` | Gang | 0,445 | 0,447 | 1.736 | 1.454 | 0,333 | 1 / 1 | — | — |
| 48604 | `BW_BL_TOM` / `BW_BL_TOM` | Gang | 0,434 | 0,436 | 1.594 | 1.277 | 0,333 | 1 / 1 | — | — |
| 48605 | `BW_BL_TRENT` / `BW_BL_TRENT` | Gang | 0,467 | 0,469 | 2.277 | 1.682 | 0,333 | 1 / 1 | — | — |
| 48606 | `BW_BL_TROY` / `BW_BL_TROY` | Gang | 0,467 | 0,469 | 2.324 | 1.663 | 0,333 | 1 / 1 | — | — |
| 48607 | `BW_BL_WADE` / `BW_BL_WADE` | Gang | 0,430 | 0,432 | 1.542 | 1.232 | 0,333 | 1 / 1 | — | — |
| 48608 | `BW_BMYBWB1` / `BW_BMYBWB1` | Dân thường | 0,431 | 0,432 | 1.522 | 1.248 | 0,333 | 1 / 1 | — | — |
| 48609 | `BW_BMYBWB2` / `BW_BMYBWB2` | Dân thường | 0,391 | 0,393 | 854 | 694 | 0,333 | 1 / 1 | — | — |
| 48610 | `BW_BMYBWB3` / `BW_BMYBWB3` | Dân thường | 0,395 | 0,396 | 874 | 780 | 0,333 | 1 / 1 | — | — |
| 48611 | `BW_CARNYWORK1` / `BW_CARNYWORK1` | Dân thường | 0,440 | 0,441 | 1.613 | 1.398 | 0,333 | 2 / 2 | — | — |
| 48612 | `BW_CARNYWORK2` / `BW_CARNYWORK2` | Dân thường | 0,423 | 0,424 | 1.381 | 1.142 | 0,333 | 1 / 2 | — | — |
| 48613 | `BW_CH_GARY` / `BW_CH_GARY` | Gang | 0,472 | 0,475 | 2.276 | 1.794 | 0,333 | 1 / 1 | — | — |
| 48614 | `BW_CH_JIMMY` / `BW_CH_JIMMY` | Model có pedtype PLAYER1/2 | 0,637 | 0,639 | 3.831 | 2.597 | 0,427 | 4 / 4 | — | — |
| 48615 | `BW_CH_MASCOT` / `BW_CH_MASCOT` | Gang | 0,442 | 0,443 | 1.532 | 1.472 | 0,333 | 2 / 2 | — | — |
| 48616 | `BW_CH_PETER` / `BW_CH_PETER` | Gang | 0,429 | 0,432 | 1.546 | 1.209 | 0,333 | 1 / 1 | — | — |
| 48617 | `BW_CHL_ASIAN` / `BW_CHL_ASIAN` | Dân thường | 0,435 | 0,436 | 1.710 | 1.260 | 0,333 | 1 / 1 | — | — |
| 48618 | `BW_CLOTHESGUY` / `BW_CLOTHESGUY` | Dân thường | 0,438 | 0,439 | 1.346 | 1.230 | 0,344 | 3 / 3 | — | — |
| 48619 | `BW_COMIC` / `BW_COMIC` | Dân thường | 0,435 | 0,438 | 1.582 | 1.254 | 0,336 | 2 / 2 | — | — |
| 48620 | `BW_CONSTRUCT1` / `BW_CONSTRUCT1` | Dân thường | 0,425 | 0,426 | 1.386 | 1.189 | 0,333 | 1 / 1 | — | — |
| 48621 | `BW_CONSTRUCT2` / `BW_CONSTRUCT2` | Dân thường | 0,442 | 0,443 | 1.610 | 1.432 | 0,333 | 1 / 1 | — | — |
| 48622 | `BW_COP01` / `BW_COP01` | Cảnh sát / quân đội / cứu hộ | 0,455 | 0,457 | 1.592 | 1.481 | 0,344 | 3 / 3 | — | — |
| 48623 | `BW_COP02` / `BW_COP02` | Cảnh sát / quân đội / cứu hộ | 0,451 | 0,453 | 1.550 | 1.419 | 0,344 | 3 / 3 | — | — |
| 48624 | `BW_COP03` / `BW_COP03` | Cảnh sát / quân đội / cứu hộ | 0,441 | 0,443 | 1.507 | 1.228 | 0,344 | 3 / 3 | — | — |
| 48625 | `BW_CRYSTAL` / `BW_CRYSTAL` | Dân thường | 0,456 | 0,457 | 2.030 | 1.566 | 0,333 | 1 / 1 | — | — |
| 48626 | `BW_DOCKWORKER` / `BW_DOCKWORKER` | Dân thường | 0,440 | 0,441 | 1.469 | 1.444 | 0,333 | 2 / 2 | — | — |
| 48627 | `BW_FIGHTINGMIDGET1` / `BW_FIGHTINGMIDGET1` | Dân thường | 0,415 | 0,416 | 1.342 | 999 | 0,333 | 1 / 1 | — | — |
| 48628 | `BW_FIGHTINGMIDGET2` / `BW_FIGHTINGMIDGET2` | Dân thường | 0,427 | 0,428 | 1.520 | 1.173 | 0,333 | 1 / 1 | — | — |
| 48629 | `BW_FIREMAN` / `BW_FIREMAN` | Cảnh sát / quân đội / cứu hộ | 0,428 | 0,430 | 1.504 | 1.189 | 0,333 | 2 / 2 | — | — |
| 48630 | `BW_FIREOWNER` / `BW_FIREOWNER` | Criminal | 0,424 | 0,424 | 1.450 | 1.122 | 0,333 | 2 / 2 | — | — |
| 48631 | `BW_FMIDGET` / `BW_FMIDGET` | Dân thường | 0,459 | 0,461 | 1.866 | 1.453 | 0,344 | 3 / 3 | — | — |
| 48632 | `BW_GCCLERK` / `BW_GCCLERK` | Dân thường | 0,416 | 0,418 | 1.282 | 1.032 | 0,333 | 2 / 2 | — | — |
| 48633 | `BW_GCOWNER` / `BW_GCOWNER` | Dân thường | 0,418 | 0,420 | 1.322 | 1.062 | 0,333 | 2 / 2 | — | — |
| 48634 | `BW_GR_HAL` / `BW_GR_HAL` | Gang | 0,427 | 0,428 | 1.474 | 1.183 | 0,333 | 1 / 1 | — | — |
| 48635 | `BW_GR_JOHNNY` / `BW_GR_JOHNNY` | Gang | 0,437 | 0,439 | 1.718 | 1.299 | 0,333 | 1 / 1 | — | — |
| 48636 | `BW_GR_LEFTY` / `BW_GR_LEFTY` | Gang | 0,418 | 0,420 | 1.353 | 1.050 | 0,333 | 1 / 1 | — | — |
| 48637 | `BW_GR_LOLA` / `BW_GR_LOLA` | Gang | 0,486 | 0,488 | 2.174 | 1.896 | 0,344 | 2 / 2 | — | — |
| 48638 | `BW_GR_LUCKY` / `BW_GR_LUCKY` | Gang | 0,434 | 0,436 | 1.613 | 1.272 | 0,333 | 1 / 1 | — | — |
| 48639 | `BW_GR_NORTON` / `BW_GR_NORTON` | Gang | 0,433 | 0,434 | 1.560 | 1.273 | 0,333 | 1 / 1 | — | — |
| 48640 | `BW_GR_PEANUT` / `BW_GR_PEANUT` | Gang | 0,430 | 0,432 | 1.573 | 1.220 | 0,333 | 1 / 1 | — | — |
| 48641 | `BW_GR_RICKY` / `BW_GR_RICKY` | Gang | 0,421 | 0,422 | 1.416 | 1.092 | 0,333 | 1 / 1 | — | — |
| 48642 | `BW_GR_VANCE` / `BW_GR_VANCE` | Gang | 0,427 | 0,428 | 1.468 | 1.186 | 0,333 | 1 / 1 | — | — |
| 48643 | `BW_HANDY` / `BW_HANDY` | Dân thường | 0,493 | 0,494 | 2.444 | 2.134 | 0,333 | 2 / 2 | — | — |
| 48644 | `BW_HOBO` / `BW_HOBO` | Dân thường | 0,411 | 0,412 | 1.274 | 927 | 0,333 | 2 / 2 | — | — |
| 48645 | `BW_INDWORKER` / `BW_INDWORKER` | Dân thường | 0,437 | 0,438 | 1.504 | 1.369 | 0,333 | 2 / 2 | — | — |
| 48646 | `BW_J_BO` / `BW_J_BO` | Gang | 0,421 | 0,424 | 1.480 | 1.076 | 0,333 | 1 / 1 | — | — |
| 48647 | `BW_J_BOB` / `BW_J_BOB` | Gang | 0,587 | 0,590 | 1.382 | 1.080 | 0,500 | 2 / 2 | — | — |
| 48648 | `BW_J_CASEY` / `BW_J_CASEY` | Gang | 0,434 | 0,436 | 1.526 | 1.301 | 0,333 | 1 / 1 | — | — |
| 48649 | `BW_J_DAMON` / `BW_J_DAMON` | Gang | 0,423 | 0,424 | 1.398 | 1.133 | 0,333 | 1 / 1 | — | — |
| 48650 | `BW_J_DAN` / `BW_J_DAN` | Gang | 0,432 | 0,434 | 1.596 | 1.235 | 0,333 | 1 / 1 | — | — |
| 48651 | `BW_J_JURI` / `BW_J_JURI` | Gang | 0,423 | 0,424 | 1.408 | 1.129 | 0,333 | 1 / 1 | — | — |
| 48652 | `BW_J_KIRBY` / `BW_J_KIRBY` | Gang | 0,426 | 0,428 | 1.508 | 1.150 | 0,333 | 1 / 1 | — | — |
| 48653 | `BW_J_LUIS` / `BW_J_LUIS` | Gang | 0,430 | 0,432 | 1.518 | 1.242 | 0,333 | 1 / 1 | — | — |
| 48654 | `BW_J_MANDY` / `BW_J_MANDY` | Gang | 0,476 | 0,479 | 2.375 | 1.838 | 0,333 | 1 / 1 | — | — |
| 48655 | `BW_J_TED` / `BW_J_TED` | Gang | 0,435 | 0,438 | 1.454 | 1.137 | 0,344 | 2 / 2 | — | — |
| 48656 | `BW_J_WRESTLER01` / `BW_J_WRESTLER01` | Gang | 0,426 | 0,428 | 1.564 | 1.134 | 0,333 | 2 / 2 | — | — |
| 48657 | `BW_MAILMAN` / `BW_MAILMAN` | Dân thường | 0,429 | 0,430 | 1.477 | 1.225 | 0,333 | 2 / 2 | — | — |
| 48658 | `BW_MERMAID` / `BW_MERMAID` | Dân thường | 0,435 | 0,436 | 1.817 | 1.210 | 0,333 | 1 / 1 | — | — |
| 48659 | `BW_MILLWORKER` / `BW_MILLWORKER` | Dân thường | 0,435 | 0,436 | 1.514 | 1.328 | 0,333 | 2 / 2 | — | — |
| 48660 | `BW_MMIDGET` / `BW_MMIDGET` | Dân thường | 0,435 | 0,438 | 1.384 | 1.158 | 0,344 | 3 / 3 | — | — |
| 48661 | `BW_MTOWNER` / `BW_MTOWNER` | Dân thường | 0,403 | 0,404 | 970 | 890 | 0,333 | 2 / 2 | — | — |
| 48662 | `BW_N_ALGERNOON` / `BW_N_ALGERNOON` | Gang | 0,440 | 0,441 | 1.634 | 1.372 | 0,334 | 2 / 2 | — | — |
| 48663 | `BW_N_BEATRICE` / `BW_N_BEATRICE` | Gang | 0,510 | 0,510 | 2.718 | 2.365 | 0,334 | 2 / 2 | — | — |
| 48664 | `BW_N_BUCKY` / `BW_N_BUCKY` | Gang | 0,453 | 0,455 | 1.731 | 1.611 | 0,333 | 1 / 2 | — | Tên texture cần xác minh: ndh3_bucky_glasses_d |
| 48665 | `BW_N_CORNELIUS` / `BW_N_CORNELIUS` | Gang | 0,444 | 0,447 | 1.630 | 1.410 | 0,336 | 2 / 2 | — | — |
| 48666 | `BW_N_DONALD` / `BW_N_DONALD` | Gang | 0,438 | 0,441 | 1.563 | 1.316 | 0,336 | 2 / 2 | — | — |
| 48667 | `BW_N_EARNEST` / `BW_N_EARNEST` | Gang | 0,384 | 0,387 | 2.140 | 1.687 | 0,252 | 4 / 4 | — | — |
| 48668 | `BW_N_FATTY` / `BW_N_FATTY` | Gang | 0,447 | 0,449 | 1.570 | 1.487 | 0,336 | 2 / 3 | — | — |
| 48669 | `BW_N_MELVIN` / `BW_N_MELVIN` | Gang | 0,449 | 0,451 | 1.584 | 1.525 | 0,336 | 2 / 2 | — | — |
| 48670 | `BW_N_THAD` / `BW_N_THAD` | Gang | 0,441 | 0,443 | 1.593 | 1.369 | 0,336 | 2 / 2 | — | — |
| 48671 | `BW_NH_RES1` / `BW_NH_RES1` | Dân thường | 0,397 | 0,398 | 888 | 811 | 0,333 | 2 / 2 | — | — |
| 48672 | `BW_NH_RES2` / `BW_NH_RES2` | Dân thường | 0,397 | 0,398 | 880 | 801 | 0,333 | 2 / 2 | — | — |
| 48673 | `BW_NH_RES3` / `BW_NH_RES3` | Dân thường | 0,403 | 0,404 | 976 | 894 | 0,333 | 2 / 2 | — | — |
| 48674 | `BW_OLDMAN2` / `BW_OLDMAN2` | Dân thường | 0,403 | 0,404 | 1.018 | 884 | 0,333 | 2 / 2 | — | — |
| 48675 | `BW_PAINTEDMAN` / `BW_PAINTEDMAN` | Dân thường | 0,438 | 0,439 | 1.806 | 1.274 | 0,333 | 1 / 1 | — | — |
| 48676 | `BW_PF_EDWARD` / `BW_PF_EDWARD` | Cảnh sát / quân đội / cứu hộ | 0,481 | 0,484 | 2.334 | 1.889 | 0,336 | 2 / 2 | — | — |
| 48677 | `BW_PF_KARL` / `BW_PF_KARL` | Cảnh sát / quân đội / cứu hộ | 0,466 | 0,467 | 2.214 | 1.683 | 0,333 | 1 / 1 | — | — |
| 48678 | `BW_PF_MAX` / `BW_PF_MAX` | Cảnh sát / quân đội / cứu hộ | 0,465 | 0,467 | 2.176 | 1.677 | 0,333 | 1 / 1 | — | — |
| 48679 | `BW_PF_SETH` / `BW_PF_SETH` | Cảnh sát / quân đội / cứu hộ | 0,462 | 0,463 | 2.150 | 1.641 | 0,333 | 1 / 1 | — | — |
| 48680 | `BW_PNKBARBER` / `BW_PNKBARBER` | Dân thường | 0,503 | 0,506 | 1.837 | 1.736 | 0,375 | 2 / 2 | — | — |
| 48681 | `BW_POORMAN2` / `BW_POORMAN2` | Dân thường | 0,338 | 0,342 | 1.442 | 1.084 | 0,250 | 2 / 3 | — | — |
| 48682 | `BW_POORWOMAN` / `BW_POORWOMAN` | Dân thường | 0,542 | 0,543 | 1.540 | 1.362 | 0,438 | 6 / 2 | — | — |
| 48683 | `BW_PRP_BIF` / `BW_PRP_BIF` | Gang | 0,422 | 0,424 | 1.400 | 1.115 | 0,333 | 1 / 1 | — | — |
| 48684 | `BW_PRP_BRYCE` / `BW_PRP_BRYCE` | Gang | 0,433 | 0,434 | 1.479 | 1.302 | 0,333 | 1 / 1 | — | — |
| 48685 | `BW_PRP_CHAD` / `BW_PRP_CHAD` | Gang | 0,430 | 0,432 | 1.490 | 1.245 | 0,333 | 1 / 1 | — | — |
| 48686 | `BW_PRP_DARBY` / `BW_PRP_DARBY` | Gang | 0,437 | 0,439 | 1.696 | 1.315 | 0,333 | 1 / 1 | — | — |
| 48687 | `BW_PRP_GORD` / `BW_PRP_GORD` | Gang | 0,438 | 0,439 | 1.649 | 1.336 | 0,333 | 1 / 1 | — | — |
| 48688 | `BW_PRP_JUSTIN` / `BW_PRP_JUSTIN` | Gang | 0,444 | 0,445 | 1.663 | 1.454 | 0,333 | 1 / 1 | — | — |
| 48689 | `BW_PRP_PARKER` / `BW_PRP_PARKER` | Gang | 0,426 | 0,428 | 1.428 | 1.190 | 0,333 | 1 / 1 | — | — |
| 48690 | `BW_PRP_PINKY` / `BW_PRP_PINKY` | Gang | 0,476 | 0,479 | 2.179 | 1.695 | 0,344 | 2 / 2 | — | — |
| 48691 | `BW_PRP_TAD` / `BW_PRP_TAD` | Gang | 0,440 | 0,441 | 1.680 | 1.379 | 0,333 | 1 / 1 | — | — |
| 48692 | `BW_RECORD` / `BW_RECORD` | Dân thường | 0,417 | 0,418 | 1.314 | 1.049 | 0,333 | 1 / 1 | — | — |
| 48693 | `BW_RICHM1` / `BW_RICHM1` | Dân thường | 0,397 | 0,398 | 958 | 783 | 0,333 | 1 / 1 | — | — |
| 48694 | `BW_RICHM2` / `BW_RICHM2` | Dân thường | 0,400 | 0,402 | 900 | 868 | 0,333 | 1 / 1 | — | — |
| 48695 | `BW_RICHM3` / `BW_RICHM3` | Dân thường | 0,410 | 0,412 | 1.209 | 944 | 0,333 | 1 / 1 | — | — |
| 48696 | `BW_RICHW1` / `BW_RICHW1` | Dân thường | 0,429 | 0,430 | 1.566 | 1.187 | 0,333 | 2 / 2 | — | — |
| 48697 | `BW_RICHW2` / `BW_RICHW2` | Dân thường | 0,417 | 0,418 | 1.302 | 1.039 | 0,333 | 2 / 2 | — | — |
| 48698 | `BW_S_ASIANGIRL` / `BW_S_ASIANGIRL` | Dân thường | 0,445 | 0,447 | 1.781 | 1.434 | 0,333 | 1 / 1 | — | — |
| 48699 | `BW_S_IVAN` / `BW_S_IVAN` | Dân thường | 0,319 | 0,322 | 1.016 | 863 | 0,250 | 1 / 1 | — | — |
| 48700 | `BW_S_TREVOR` / `BW_S_TREVOR` | Dân thường | 0,320 | 0,322 | 1.032 | 878 | 0,250 | 1 / 1 | — | — |
| 48701 | `BW_SCH_ART` / `BW_SCH_ART` | Dân thường | 0,464 | 0,465 | 2.120 | 1.677 | 0,333 | 2 / 2 | — | — |
| 48702 | `BW_SCH_AUTOSHOP` / `BW_SCH_AUTOSHOP` | Dân thường | 0,427 | 0,428 | 1.454 | 1.194 | 0,333 | 2 / 2 | — | — |
| 48703 | `BW_SCH_BIOLOGY` / `BW_SCH_BIOLOGY` | Dân thường | 0,434 | 0,436 | 1.594 | 1.265 | 0,333 | 2 / 4 | — | — |
| 48704 | `BW_SCH_CHEM` / `BW_SCH_CHEM` | Dân thường | 0,446 | 0,447 | 1.594 | 1.513 | 0,333 | 2 / 2 | — | — |
| 48705 | `BW_SCH_EDNA` / `BW_SCH_EDNA` | Dân thường | 0,431 | 0,432 | 1.554 | 1.236 | 0,333 | 2 / 2 | — | — |
| 48706 | `BW_SCH_ENGLISH` / `BW_SCH_ENGLISH` | Dân thường | 0,447 | 0,447 | 1.632 | 1.524 | 0,333 | 2 / 2 | — | — |
| 48707 | `BW_SCH_GEO` / `BW_SCH_GEO` | Dân thường | 0,443 | 0,445 | 1.707 | 1.422 | 0,333 | 1 / 1 | — | — |
| 48708 | `BW_SCH_GYM` / `BW_SCH_GYM` | Dân thường | 0,433 | 0,436 | 1.579 | 1.272 | 0,333 | 2 / 2 | — | — |
| 48709 | `BW_SCH_HALLM` / `BW_SCH_HALLM` | Dân thường | 0,427 | 0,428 | 1.475 | 1.189 | 0,333 | 2 / 2 | — | — |
| 48710 | `BW_SCH_HISTORY` / `BW_SCH_HISTORY` | Dân thường | 0,447 | 0,449 | 1.740 | 1.488 | 0,333 | 2 / 2 | — | — |
| 48711 | `BW_SCH_JANITOR` / `BW_SCH_JANITOR` | Dân thường | 0,426 | 0,428 | 1.472 | 1.172 | 0,333 | 2 / 2 | — | — |
| 48712 | `BW_SCH_LIBRARIAN` / `BW_SCH_LIBRARIAN` | Dân thường | 0,431 | 0,432 | 1.526 | 1.250 | 0,333 | 2 / 2 | — | — |
| 48713 | `BW_SCH_MATH` / `BW_SCH_MATH` | Dân thường | 0,434 | 0,436 | 1.516 | 1.312 | 0,333 | 2 / 2 | — | — |
| 48714 | `BW_SCH_MUSIC` / `BW_SCH_MUSIC` | Dân thường | 0,459 | 0,461 | 1.942 | 1.647 | 0,333 | 1 / 1 | — | — |
| 48715 | `BW_SCH_NURSE` / `BW_SCH_NURSE` | Dân thường | 0,343 | 0,346 | 1.436 | 1.193 | 0,250 | 2 / 2 | — | — |
| 48716 | `BW_SCH_PRINCIPAL` / `BW_SCH_PRINCIPAL` | Gang | 0,443 | 0,445 | 1.734 | 1.412 | 0,333 | 2 / 2 | — | — |
| 48717 | `BW_SCH_SECRETARY` / `BW_SCH_SECRETARY` | Dân thường | 0,449 | 0,449 | 1.885 | 1.461 | 0,333 | 2 / 2 | — | — |
| 48718 | `BW_SCS_ANGIE` / `BW_SCS_ANGIE` | Gang | 0,476 | 0,479 | 2.077 | 1.890 | 0,336 | 2 / 2 | — | — |
| 48719 | `BW_SCS_CHRISTY` / `BW_SCS_CHRISTY` | Gang | 0,464 | 0,465 | 2.218 | 1.649 | 0,333 | 1 / 1 | — | — |
| 48720 | `BW_SCS_CONSTANTINOS` / `BW_SCS_CONSTANTINOS` | Gang | 0,405 | 0,406 | 1.098 | 900 | 0,333 | 1 / 1 | — | — |
| 48721 | `BW_SCS_EUNICE` / `BW_SCS_EUNICE` | Gang | 0,432 | 0,434 | 1.436 | 1.301 | 0,333 | 1 / 1 | — | — |
| 48722 | `BW_SCS_GORDON` / `BW_SCS_GORDON` | Gang | 0,431 | 0,432 | 1.442 | 1.276 | 0,333 | 1 / 1 | — | — |
| 48723 | `BW_SCS_IVAN` / `BW_SCS_IVAN` | Gang | 0,402 | 0,404 | 1.016 | 863 | 0,333 | 1 / 1 | — | — |
| 48724 | `BW_SCS_LANCE` / `BW_SCS_LANCE` | Gang | 0,422 | 0,424 | 1.412 | 1.119 | 0,333 | 1 / 1 | — | — |
| 48725 | `BW_SCS_RAY` / `BW_SCS_RAY` | Gang | 0,421 | 0,422 | 1.396 | 1.098 | 0,333 | 1 / 1 | — | — |
| 48726 | `BW_SCS_TREVOR` / `BW_SCS_TREVOR` | Gang | 0,403 | 0,404 | 1.032 | 878 | 0,333 | 1 / 1 | — | — |
| 48727 | `BW_SKELETONMAN` / `BW_SKELETONMAN` | Dân thường | 0,483 | 0,484 | 1.854 | 1.310 | 0,375 | 3 / 3 | — | — |
| 48728 | `BW_T_DUNCAN` / `BW_T_DUNCAN` | Gang | 0,419 | 0,420 | 1.354 | 1.066 | 0,333 | 1 / 1 | — | — |
| 48729 | `BW_T_EDGAR` / `BW_T_EDGAR` | Gang | 0,451 | 0,453 | 1.936 | 1.495 | 0,333 | 1 / 1 | — | — |
| 48730 | `BW_T_GURNEY` / `BW_T_GURNEY` | Gang | 0,420 | 0,422 | 1.408 | 1.078 | 0,333 | 1 / 1 | — | — |
| 48731 | `BW_T_HENRY` / `BW_T_HENRY` | Gang | 0,432 | 0,434 | 1.596 | 1.243 | 0,333 | 1 / 1 | — | — |
| 48732 | `BW_T_JERRY` / `BW_T_JERRY` | Gang | 0,425 | 0,426 | 1.471 | 1.142 | 0,333 | 1 / 1 | — | — |
| 48733 | `BW_T_LEON` / `BW_T_LEON` | Gang | 0,424 | 0,426 | 1.442 | 1.149 | 0,333 | 1 / 1 | — | — |
| 48734 | `BW_T_OMAR` / `BW_T_OMAR` | Gang | 0,422 | 0,424 | 1.470 | 1.084 | 0,333 | 1 / 1 | — | — |
| 48735 | `BW_T_OTTO` / `BW_T_OTTO` | Gang | 0,336 | 0,340 | 1.408 | 1.071 | 0,250 | 1 / 1 | — | — |
| 48736 | `BW_T_ZOE` / `BW_T_ZOE` | Gang | 0,490 | 0,492 | 1.914 | 1.449 | 0,375 | 2 / 2 | — | — |
| 48737 | `BW_T_ZOEU` / `BW_T_ZOEU` | Gang | 0,501 | 0,504 | 2.060 | 1.615 | 0,375 | 2 / 2 | — | — |
| 48738 | `BW_TATTOO` / `BW_TATTOO` | Dân thường | 0,432 | 0,434 | 1.602 | 1.237 | 0,333 | 2 / 2 | — | — |
| 48739 | `BW_WFYBW1` / `BW_WFYBW1` | Dân thường | 0,339 | 0,342 | 1.322 | 1.155 | 0,250 | 1 / 1 | — | — |
| 48740 | `BW_WFYBW2` / `BW_WFYBW2` | Dân thường | 0,335 | 0,338 | 1.276 | 1.095 | 0,250 | 1 / 1 | — | — |
| 48741 | `BW_WMYAS2` / `BW_WMYAS2` | Dân thường | 0,438 | 0,439 | 1.386 | 1.453 | 0,333 | 1 / 1 | — | — |
| 48742 | `BW_WMYBIKE` / `BW_WMYBIKE` | Dân thường | 0,426 | 0,428 | 1.430 | 1.191 | 0,333 | 1 / 1 | — | — |
| 48743 | `BW_WMYBWB1` / `BW_WMYBWB1` | Dân thường | 0,432 | 0,434 | 1.336 | 1.348 | 0,333 | 1 / 1 | — | — |
| 48744 | `BW_WMYBWB2` / `BW_WMYBWB2` | Dân thường | 0,396 | 0,398 | 968 | 761 | 0,333 | 1 / 1 | — | — |
| 48745 | `BW_WMYBWPB` / `BW_WMYBWPB` | Dân thường | 0,115 | 0,117 | 1.316 | 1.349 | 0,016 | 2 / 1 | — | — |
| 48746 | `BW_WORKMAN` / `BW_WORKMAN` | Dân thường | 0,439 | 0,439 | 1.426 | 1.441 | 0,333 | 1 / 1 | — | — |
| 48747 | `BW_XMAS_ELFF` / `BW_XMAS_ELFF` | Dân thường | 0,435 | 0,438 | 1.463 | 1.129 | 0,344 | 2 / 2 | — | — |
| 48748 | `BW_XMAS_ELFM` / `BW_XMAS_ELFM` | Dân thường | 0,423 | 0,424 | 1.450 | 1.109 | 0,333 | 1 / 1 | — | — |
| 48749 | `BW_XMAS_RUDY` / `BW_XMAS_RUDY` | Dân thường | 0,435 | 0,436 | 1.586 | 1.298 | 0,333 | 1 / 1 | — | — |
| 48750 | `BW_XMAS_SANTA` / `BW_XMAS_SANTA` | Dân thường | 0,443 | 0,443 | 1.720 | 1.411 | 0,333 | 1 / 1 | — | — |
| 48751 | `MW_ARMY` / `MW_ARMY` | Cảnh sát / quân đội / cứu hộ | 0,104 | 0,105 | 1.145 | 1.100 | 0,021 | 1 / 1 | — | — |
| 48752 | `MW_BFOH` / `MW_BFOH` | Dân thường | 0,091 | 0,092 | 1.111 | 846 | 0,021 | 1 / 1 | — | — |
| 48753 | `MW_BFYAPRO` / `MW_BFYAPRO` | Prostitute | 0,083 | 0,084 | 966 | 755 | 0,021 | 1 / 1 | — | — |
| 48754 | `MW_BFYBE2` / `MW_BFYBE2` | Dân thường | 0,113 | 0,113 | 1.308 | 1.218 | 0,021 | 1 / 1 | — | — |
| 48755 | `MW_BFYBUW` / `MW_BFYBUW` | Dân thường | 0,094 | 0,096 | 983 | 961 | 0,021 | 1 / 1 | — | — |
| 48756 | `MW_BFYBUW2` / `MW_BFYBUW2` | Dân thường | 0,109 | 0,109 | 1.129 | 1.204 | 0,021 | 1 / 1 | — | — |
| 48757 | `MW_BFYDCG` / `MW_BFYDCG` | Dân thường | 0,088 | 0,090 | 1.084 | 797 | 0,021 | 1 / 1 | — | — |
| 48758 | `MW_BFYPIRI` / `MW_BFYPIRI` | Dân thường | 0,088 | 0,090 | 904 | 879 | 0,021 | 1 / 1 | — | — |
| 48759 | `MW_BFYSGW` / `MW_BFYSGW` | Dân thường | 0,089 | 0,090 | 904 | 890 | 0,021 | 1 / 1 | — | — |
| 48760 | `MW_BIKER01` / `MW_BIKER01` | Gang | 0,187 | 0,189 | 1.768 | 1.467 | 0,073 | 3 / 5 | — | Tên texture cần xác minh: wmycr |
| 48761 | `MW_BIKER02` / `MW_BIKER02` | Gang | 0,196 | 0,197 | 1.869 | 1.613 | 0,073 | 3 / 6 | — | — |
| 48762 | `MW_BIKER03` / `MW_BIKER03` | Gang | 0,134 | 0,137 | 1.485 | 1.303 | 0,034 | 3 / 3 | — | — |
| 48763 | `MW_BMORH` / `MW_BMORH` | Dân thường | 0,092 | 0,094 | 1.145 | 961 | 0,016 | 1 / 1 | — | — |
| 48764 | `MW_BMYAG` / `MW_BMYAG` | Dân thường | 0,095 | 0,096 | 1.079 | 944 | 0,021 | 1 / 1 | — | — |
| 48765 | `MW_BMYBE2` / `MW_BMYBE2` | Dân thường | 0,087 | 0,090 | 1.140 | 875 | 0,016 | 1 / 1 | — | — |
| 48766 | `MW_BMYBOBO` / `MW_BMYBOBO` | Dân thường | 0,090 | 0,092 | 1.021 | 877 | 0,021 | 1 / 1 | — | — |
| 48767 | `MW_BMYBUK` / `MW_BMYBUK` | Dân thường | 0,085 | 0,086 | 870 | 818 | 0,021 | 1 / 1 | — | — |
| 48768 | `MW_BMYCZ` / `MW_BMYCZ` | Dân thường | 0,101 | 0,102 | 1.129 | 1.051 | 0,021 | 1 / 1 | — | — |
| 48769 | `MW_BMYMOUN3` / `MW_BMYMOUN3` | Dân thường | 0,085 | 0,088 | 1.107 | 953 | 0,010 | 1 / 1 | — | — |
| 48770 | `MW_BMYPBOX` / `MW_BMYPBOX` | Dân thường | 0,086 | 0,088 | 1.228 | 928 | 0,010 | 1 / 1 | — | — |
| 48771 | `MW_BMYRG` / `MW_BMYRG` | Dân thường | 0,101 | 0,104 | 1.138 | 1.055 | 0,021 | 1 / 1 | — | — |
| 48772 | `MW_BMYRG2` / `MW_BMYRG2` | Dân thường | 0,110 | 0,111 | 1.265 | 1.173 | 0,021 | 1 / 1 | — | — |
| 48773 | `MW_BMYSWT` / `MW_BMYSWT` | Dân thường | 0,100 | 0,102 | 1.106 | 1.038 | 0,021 | 1 / 1 | — | — |
| 48774 | `MW_BMYUEGG` / `MW_BMYUEGG` | Dân thường | 0,106 | 0,107 | 1.127 | 1.147 | 0,021 | 1 / 1 | — | — |
| 48775 | `MW_BMYVDK` / `MW_BMYVDK` | Dân thường | 0,082 | 0,084 | 1.030 | 803 | 0,016 | 1 / 1 | — | — |
| 48776 | `MW_BURGSHOT` / `MW_BURGSHOT` | Dân thường | 0,171 | 0,174 | 2.086 | 1.677 | 0,042 | 1 / 1 | — | — |
| 48777 | `MW_CABDRIVER` / `MW_CABDRIVER` | Dân thường | 0,086 | 0,088 | 991 | 808 | 0,021 | 1 / 1 | — | — |
| 48778 | `MW_CABDRIVER2` / `MW_CABDRIVER2` | Dân thường | 0,085 | 0,086 | 940 | 808 | 0,021 | 1 / 1 | — | — |
| 48779 | `MW_COP` / `MW_COP` | Cảnh sát / quân đội / cứu hộ | 0,098 | 0,100 | 1.121 | 1.000 | 0,021 | 1 / 1 | — | — |
| 48780 | `MW_DICKHEAD1` / `MW_DICKHEAD1` | Gang | 0,100 | 0,102 | 1.140 | 1.082 | 0,018 | 2 / 2 | — | — |
| 48781 | `MW_DICKHEAD2` / `MW_DICKHEAD2` | Gang | 0,107 | 0,107 | 1.124 | 1.004 | 0,029 | 2 / 4 | — | — |
| 48782 | `MW_DICKHEAD3` / `MW_DICKHEAD3` | Gang | 0,164 | 0,166 | 1.158 | 1.059 | 0,083 | 1 / 1 | — | — |
| 48783 | `MW_DJ` / `MW_DJ` | Dân thường | 0,155 | 0,156 | 1.748 | 1.472 | 0,042 | 1 / 4 | — | — |
| 48784 | `MW_FBI` / `MW_FBI` | Cảnh sát / quân đội / cứu hộ | 0,088 | 0,090 | 1.002 | 843 | 0,021 | 1 / 2 | — | — |
| 48785 | `MW_FIREMAN` / `MW_FIREMAN` | Cảnh sát / quân đội / cứu hộ | 0,100 | 0,102 | 1.049 | 1.064 | 0,021 | 1 / 1 | — | — |
| 48786 | `MW_HFYBE3` / `MW_HFYBE3` | Dân thường | 0,118 | 0,121 | 1.231 | 1.129 | 0,031 | 2 / 2 | — | — |
| 48787 | `MW_HFYPIRI` / `MW_HFYPIRI` | Dân thường | 0,088 | 0,090 | 904 | 881 | 0,021 | 1 / 1 | — | — |
| 48788 | `MW_HFYSPRO` / `MW_HFYSPRO` | Prostitute | 0,122 | 0,123 | 1.554 | 1.320 | 0,021 | 1 / 1 | — | — |
| 48789 | `MW_HMOTOUR` / `MW_HMOTOUR` | Dân thường | 0,098 | 0,100 | 1.084 | 968 | 0,022 | 2 / 3 | — | — |
| 48790 | `MW_HMYBE2` / `MW_HMYBE2` | Dân thường | 0,085 | 0,088 | 1.106 | 835 | 0,016 | 1 / 1 | — | — |
| 48791 | `MW_HMYMOUN` / `MW_HMYMOUN` | Dân thường | 0,085 | 0,088 | 1.107 | 953 | 0,010 | 1 / 1 | — | — |
| 48792 | `MW_HMYPLT` / `MW_HMYPLT` | Dân thường | 0,090 | 0,092 | 990 | 884 | 0,021 | 1 / 1 | — | — |
| 48793 | `MW_MARSHAL` / `MW_MARSHAL` | Cảnh sát / quân đội / cứu hộ | 0,102 | 0,104 | 1.164 | 1.059 | 0,021 | 1 / 1 | — | — |
| 48794 | `MW_MECH` / `MW_MECH` | Dân thường | 0,089 | 0,092 | 1.019 | 956 | 0,016 | 1 / 2 | — | — |
| 48795 | `MW_MEDIC` / `MW_MEDIC` | Cảnh sát / quân đội / cứu hộ | 0,090 | 0,092 | 1.024 | 865 | 0,021 | 1 / 1 | — | — |
| 48796 | `MW_MLG1` / `MW_MLG1` | Gang | 0,229 | 0,230 | 2.775 | 1.938 | 0,073 | 2 / 2 | — | — |
| 48797 | `MW_MLG2` / `MW_MLG2` | Gang | 0,101 | 0,104 | 1.090 | 1.066 | 0,021 | 1 / 2 | — | — |
| 48798 | `MW_MLG3` / `MW_MLG3` | Gang | 0,103 | 0,105 | 1.120 | 1.097 | 0,021 | 1 / 1 | — | — |
| 48799 | `MW_MLLMYAP` / `MW_MLLMYAP` | Dân thường | 0,176 | 0,178 | 2.324 | 2.106 | 0,021 | 1 / 1 | — | — |
| 48800 | `MW_MZTN1` / `MW_MZTN1` | Gang | 0,081 | 0,084 | 996 | 799 | 0,016 | 1 / 2 | — | — |
| 48801 | `MW_MZTN2` / `MW_MZTN2` | Gang | 0,103 | 0,104 | 1.149 | 1.076 | 0,021 | 1 / 2 | — | — |
| 48802 | `MW_MZTN3` / `MW_MZTN3` | Gang | 0,105 | 0,105 | 1.129 | 1.125 | 0,021 | 1 / 1 | — | — |
| 48803 | `MW_OFMOTR1` / `MW_OFMOTR1` | Dân thường | 0,091 | 0,092 | 1.026 | 889 | 0,021 | 1 / 1 | — | — |
| 48804 | `MW_OFYBE` / `MW_OFYBE` | Dân thường | 0,107 | 0,109 | 1.242 | 1.134 | 0,021 | 1 / 1 | — | — |
| 48805 | `MW_OFYHG` / `MW_OFYHG` | Dân thường | 0,106 | 0,107 | 1.234 | 1.102 | 0,021 | 1 / 1 | — | — |
| 48806 | `MW_OMMBU` / `MW_OMMBU` | Dân thường | 0,085 | 0,086 | 872 | 820 | 0,021 | 1 / 1 | — | — |
| 48807 | `MW_OMOHA` / `MW_OMOHA` | Dân thường | 0,085 | 0,086 | 1.006 | 762 | 0,021 | 1 / 2 | — | — |
| 48808 | `MW_OMYBE` / `MW_OMYBE` | Dân thường | 0,094 | 0,096 | 1.146 | 900 | 0,021 | 1 / 1 | — | — |
| 48809 | `MW_PIMP` / `MW_PIMP` | Dân thường | 0,101 | 0,102 | 1.070 | 1.055 | 0,021 | 2 / 2 | — | — |
| 48810 | `MW_PREACHER` / `MW_PREACHER` | Dân thường | 0,086 | 0,088 | 928 | 820 | 0,021 | 1 / 2 | — | — |
| 48811 | `MW_PUNK1` / `MW_PUNK1` | Gang | 0,088 | 0,090 | 999 | 835 | 0,021 | 1 / 1 | — | — |
| 48812 | `MW_PUNK2` / `MW_PUNK2` | Gang | 0,147 | 0,150 | 1.656 | 1.362 | 0,042 | 1 / 1 | — | — |
| 48813 | `MW_PUNK3` / `MW_PUNK3` | Gang | 0,102 | 0,104 | 1.198 | 1.046 | 0,021 | 1 / 1 | — | — |
| 48814 | `MW_SOMYRG` / `MW_SOMYRG` | Dân thường | 0,103 | 0,104 | 1.104 | 1.100 | 0,021 | 1 / 1 | — | — |
| 48815 | `MW_SWAT` / `MW_SWAT` | Cảnh sát / quân đội / cứu hộ | 0,101 | 0,102 | 1.097 | 1.057 | 0,021 | 1 / 1 | — | — |
| 48816 | `MW_VHMYPP` / `MW_VHMYPP` | Dân thường | 0,088 | 0,090 | 966 | 860 | 0,021 | 1 / 1 | — | — |
| 48817 | `MW_WFOYA` / `MW_WFOYA` | Dân thường | 0,080 | 0,082 | 912 | 720 | 0,021 | 1 / 1 | — | — |
| 48818 | `MW_WFYBE2` / `MW_WFYBE2` | Dân thường | 0,102 | 0,105 | 1.242 | 1.134 | 0,016 | 1 / 1 | — | — |
| 48819 | `MW_WFYBPRO` / `MW_WFYBPRO` | Prostitute | 0,092 | 0,094 | 1.018 | 819 | 0,025 | 2 / 2 | — | — |
| 48820 | `MW_WFYBUW` / `MW_WFYBUW` | Dân thường | 0,109 | 0,111 | 1.165 | 1.195 | 0,021 | 1 / 2 | — | — |
| 48821 | `MW_WFYBUW2` / `MW_WFYBUW2` | Dân thường | 0,088 | 0,090 | 978 | 848 | 0,021 | 1 / 1 | — | — |
| 48822 | `MW_WFYBUW3` / `MW_WFYBUW3` | Dân thường | 0,096 | 0,098 | 986 | 1.011 | 0,021 | 1 / 1 | — | — |
| 48823 | `MW_WFYCLA` / `MW_WFYCLA` | Dân thường | 0,112 | 0,113 | 1.198 | 1.251 | 0,021 | 1 / 1 | — | — |
| 48824 | `MW_WFYCPRO` / `MW_WFYCPRO` | Prostitute | 0,105 | 0,105 | 1.105 | 1.139 | 0,021 | 1 / 1 | — | — |
| 48825 | `MW_WFYFRAT` / `MW_WFYFRAT` | Dân thường | 0,199 | 0,201 | 1.356 | 1.460 | 0,094 | 2 / 2 | — | — |
| 48826 | `MW_WFYFRAT2` / `MW_WFYFRAT2` | Dân thường | 0,196 | 0,199 | 1.337 | 1.405 | 0,094 | 2 / 3 | — | — |
| 48827 | `MW_WFYFWD` / `MW_WFYFWD` | Dân thường | 0,088 | 0,090 | 1.007 | 830 | 0,021 | 1 / 1 | — | — |
| 48828 | `MW_WFYMYO2` / `MW_WFYMYO2` | Dân thường | 0,107 | 0,109 | 1.270 | 1.126 | 0,021 | 1 / 1 | — | — |
| 48829 | `MW_WFYPIRI` / `MW_WFYPIRI` | Dân thường | 0,088 | 0,090 | 904 | 879 | 0,021 | 1 / 1 | — | — |
| 48830 | `MW_WFYRIW` / `MW_WFYRIW` | Dân thường | 0,107 | 0,109 | 1.138 | 1.148 | 0,022 | 2 / 2 | — | — |
| 48831 | `MW_WFYRIWB` / `MW_WFYRIWB` | Dân thường | 0,107 | 0,109 | 1.136 | 1.147 | 0,022 | 2 / 2 | — | — |
| 48832 | `MW_WFYRO3` / `MW_WFYRO3` | Dân thường | 0,118 | 0,121 | 1.317 | 1.111 | 0,031 | 2 / 2 | — | — |
| 48833 | `MW_WFYSGW` / `MW_WFYSGW` | Dân thường | 0,088 | 0,090 | 904 | 879 | 0,021 | 1 / 1 | — | — |
| 48834 | `MW_WFYSX` / `MW_WFYSX` | Dân thường | 0,099 | 0,100 | 1.102 | 1.018 | 0,021 | 1 / 1 | — | — |
| 48835 | `MW_WFYZPRO` / `MW_WFYZPRO` | Prostitute | 0,116 | 0,117 | 1.214 | 1.320 | 0,021 | 1 / 1 | — | — |
| 48836 | `MW_WGYRO` / `MW_WGYRO` | Dân thường | 0,096 | 0,098 | 1.157 | 937 | 0,021 | 1 / 1 | — | — |
| 48837 | `MW_WMMBU` / `MW_WMMBU` | Dân thường | 0,085 | 0,086 | 872 | 820 | 0,021 | 1 / 1 | — | — |
| 48838 | `MW_WMOAH` / `MW_WMOAH` | Dân thường | 0,128 | 0,129 | 1.651 | 1.384 | 0,021 | 1 / 1 | — | — |
| 48839 | `MW_WMOBU` / `MW_WMOBU` | Dân thường | 0,084 | 0,086 | 964 | 762 | 0,021 | 1 / 1 | — | — |
| 48840 | `MW_WMOCH` / `MW_WMOCH` | Dân thường | 0,145 | 0,146 | 1.936 | 1.625 | 0,021 | 1 / 1 | — | — |
| 48841 | `MW_WMOPS` / `MW_WMOPS` | Dân thường | 0,090 | 0,092 | 1.054 | 857 | 0,021 | 1 / 1 | — | — |
| 48842 | `MW_WMOZA` / `MW_WMOZA` | Dân thường | 0,102 | 0,104 | 1.148 | 1.061 | 0,021 | 1 / 1 | — | — |
| 48843 | `MW_WMYBE2` / `MW_WMYBE2` | Dân thường | 0,086 | 0,088 | 1.090 | 757 | 0,021 | 1 / 1 | — | — |
| 48844 | `MW_WMYBUK` / `MW_WMYBUK` | Dân thường | 0,085 | 0,086 | 872 | 820 | 0,021 | 1 / 1 | — | — |
| 48845 | `MW_WMYBWC` / `MW_WMYBWC` | Dân thường | 0,119 | 0,121 | 1.404 | 1.091 | 0,031 | 1 / 1 | — | — |
| 48846 | `MW_WMYCA` / `MW_WMYCA` | Dân thường | 0,094 | 0,096 | 1.038 | 935 | 0,021 | 1 / 1 | — | — |
| 48847 | `MW_WMYDRUG` / `MW_WMYDRUG` | Criminal | 0,261 | 0,264 | 2.191 | 1.755 | 0,125 | 2 / 4 | — | — |
| 48848 | `MW_WMYFJG` / `MW_WMYFJG` | Dân thường | 0,131 | 0,133 | 1.791 | 1.394 | 0,021 | 1 / 1 | — | — |
| 48849 | `MW_WMYHCA` / `MW_WMYHCA` | Dân thường | 0,115 | 0,117 | 1.350 | 1.251 | 0,021 | 1 / 1 | — | — |
| 48850 | `MW_WMYHPJ` / `MW_WMYHPJ` | Dân thường | 0,089 | 0,090 | 996 | 863 | 0,021 | 1 / 1 | — | — |
| 48851 | `MW_WMYJG2` / `MW_WMYJG2` | Dân thường | 0,096 | 0,098 | 1.252 | 1.113 | 0,010 | 1 / 1 | — | — |
| 48852 | `MW_WMYJOCK` / `MW_WMYJOCK` | Dân thường | 0,115 | 0,117 | 1.070 | 1.035 | 0,036 | 2 / 3 | — | — |
| 48853 | `MW_WMYLET` / `MW_WMYLET` | Dân thường | 0,130 | 0,131 | 1.664 | 1.427 | 0,021 | 1 / 1 | — | — |
| 48854 | `MW_WMYLFF` / `MW_WMYLFF` | Dân thường | 0,115 | 0,117 | 1.070 | 1.035 | 0,036 | 2 / 3 | — | — |
| 48855 | `MW_WMYMOUN2` / `MW_WMYMOUN2` | Dân thường | 0,085 | 0,088 | 1.107 | 953 | 0,010 | 1 / 1 | — | — |
| 48856 | `MW_WMYPG` / `MW_WMYPG` | Dân thường | 0,085 | 0,088 | 1.070 | 857 | 0,016 | 1 / 1 | — | — |
| 48857 | `MW_WMYPS` / `MW_WMYPS` | Dân thường | 0,084 | 0,086 | 942 | 770 | 0,021 | 1 / 1 | — | — |
| 48858 | `MW_WMYRG1` / `MW_WMYRG1` | Dân thường | 0,161 | 0,162 | 1.776 | 1.585 | 0,042 | 2 / 2 | — | — |
| 48859 | `MW_WMYSP` / `MW_WMYSP` | Dân thường | 0,104 | 0,105 | 1.159 | 1.092 | 0,021 | 1 / 1 | — | — |
| 48860 | `MW_WORK1` / `MW_WORK1` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48861 | `MW_WORK10` / `MW_WORK10` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48862 | `MW_WORK2` / `MW_WORK2` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48863 | `MW_WORK3` / `MW_WORK3` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48864 | `MW_WORK4` / `MW_WORK4` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48865 | `MW_WORK5` / `MW_WORK5` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48866 | `MW_WORK6` / `MW_WORK6` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48867 | `MW_WORK7` / `MW_WORK7` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48868 | `MW_WORK8` / `MW_WORK8` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48869 | `MW_WORK9` / `MW_WORK9` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 48870 | `SA_FAM4` / `SA_FAM4` | Gang | 0,098 | 0,100 | 1.105 | 1.001 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 48871 | `SA_FAM5` / `SA_FAM5` | Gang | 0,098 | 0,100 | 1.105 | 1.001 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 48872 | `SA_FAM6` / `SA_FAM6` | Gang | 0,092 | 0,094 | 987 | 932 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 48873 | `ug_bdg_wmybd1` / `ug_bdg_wmybd1` | Dân thường | 0,084 | 0,086 | 879 | 800 | 0,021 | 1 / 1 | — | — |
| 48874 | `ug_bdg_wmybd2` / `ug_bdg_wmybd2` | Dân thường | 0,085 | 0,086 | 919 | 816 | 0,021 | 1 / 1 | — | — |
| 48875 | `ug_bdg_wmybd3` / `ug_bdg_wmybd3` | Dân thường | 0,085 | 0,086 | 919 | 816 | 0,021 | 1 / 1 | — | — |
| 48876 | `psycho` / `psycho` | Dân thường | 0,182 | 0,186 | 860 | 688 | 0,125 | 1 / 1 | — | — |
| 48877 | `SA_FAM7` / `SA_FAM7` | Gang | 0,100 | 0,102 | 1.176 | 1.004 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 48878 | `SA_FAM8` / `SA_FAM8` | Gang | 0,155 | 0,158 | 1.914 | 1.422 | 0,042 | 1 / 1 | Carcer City, Los Santos | — |
| 48879 | `SA_FAM9` / `SA_FAM9` | Gang | 0,106 | 0,109 | 1.286 | 1.202 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 48880 | `lcpdm1` / `lcpdm1` | Cảnh sát / quân đội / cứu hộ | 0,112 | 0,115 | 1.264 | 1.332 | 0,016 | 1 / 1 | — | — |
| 48881 | `ccpdm1` / `ccpdm1` | Cảnh sát / quân đội / cứu hộ | 0,104 | 0,105 | 1.122 | 1.110 | 0,021 | 1 / 1 | — | — |
| 48882 | `csherm1` / `csherm1` | Cảnh sát / quân đội / cứu hộ | 0,097 | 0,100 | 1.106 | 1.082 | 0,016 | 1 / 1 | — | — |
| 48883 | `atpdm1` / `atpdm1` | Cảnh sát / quân đội / cứu hộ | 0,097 | 0,098 | 1.013 | 1.015 | 0,021 | 1 / 1 | — | — |
| 48884 | `mwpdm1` / `mwpdm1` | Cảnh sát / quân đội / cứu hộ | 0,093 | 0,096 | 1.000 | 1.033 | 0,016 | 1 / 2 | — | — |
| 48885 | `lvpdm1` / `lvpdm1` | Cảnh sát / quân đội / cứu hộ | 0,098 | 0,100 | 1.026 | 1.034 | 0,021 | 1 / 1 | — | — |
| 48886 | `sfpdm1` / `sfpdm1` | Cảnh sát / quân đội / cứu hộ | 0,092 | 0,094 | 986 | 924 | 0,021 | 1 / 1 | — | — |
| 48887 | `bwpdm1` / `bwpdm1` | Cảnh sát / quân đội / cứu hộ | 0,474 | 0,477 | 1.944 | 1.744 | 0,344 | 2 / 2 | — | — |
| 48888 | `ul_army` / `ul_army` | Cảnh sát / quân đội / cứu hộ | 0,101 | 0,102 | 1.095 | 1.057 | 0,021 | 1 / 1 | — | — |
| 48889 | `ul_cop` / `ul_cop` | Cảnh sát / quân đội / cứu hộ | 0,375 | 0,377 | 3.628 | 3.509 | 0,125 | 1 / 1 | — | — |
| 48890 | `ul_fireman` / `ul_fireman` | Cảnh sát / quân đội / cứu hộ | 0,100 | 0,102 | 1.065 | 1.046 | 0,021 | 1 / 1 | — | — |
| 48891 | `ul_medic` / `ul_medic` | Cảnh sát / quân đội / cứu hộ | 0,090 | 0,092 | 1.024 | 865 | 0,021 | 1 / 1 | — | — |
| 48892 | `ul_swat` / `ul_swat` | Cảnh sát / quân đội / cứu hộ | 0,101 | 0,102 | 1.097 | 1.057 | 0,021 | 1 / 1 | — | — |
| 48893 | `dsherm1` / `dsherm1` | Cảnh sát / quân đội / cứu hộ | 0,102 | 0,104 | 1.106 | 1.082 | 0,021 | 1 / 1 | — | — |
| 48894 | `sa_ballas4` / `sa_ballas4` | Gang | 0,101 | 0,104 | 1.161 | 1.044 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 48895 | `sa_ballas5` / `sa_ballas5` | Gang | 0,147 | 0,150 | 1.737 | 1.333 | 0,042 | 1 / 1 | Carcer City, Los Santos | — |
| 48896 | `sa_ballas6` / `sa_ballas6` | Gang | 0,156 | 0,158 | 1.872 | 1.446 | 0,042 | 1 / 1 | Carcer City, Los Santos | — |
| 48897 | `sa_ballas7` / `sa_ballas7` | Gang | 0,139 | 0,141 | 1.646 | 1.551 | 0,023 | 2 / 3 | Carcer City, Los Santos | — |
| 48898 | `sa_ballas8` / `sa_ballas8` | Gang | 0,103 | 0,104 | 1.134 | 1.087 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 48899 | `sa_ballas9` / `sa_ballas9` | Gang | 0,102 | 0,104 | 1.171 | 1.046 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 48900 | `atpdh1` / `atpdh1` | Cảnh sát / quân đội / cứu hộ | 0,134 | 0,137 | 1.614 | 1.459 | 0,023 | 2 / 3 | — | — |
| 48901 | `ccpdh1` / `ccpdh1` | Cảnh sát / quân đội / cứu hộ | 0,131 | 0,133 | 1.562 | 1.420 | 0,023 | 2 / 4 | — | — |
| 48902 | `cmpdh1` / `cmpdh1` | Cảnh sát / quân đội / cứu hộ | 0,132 | 0,135 | 1.578 | 1.437 | 0,023 | 2 / 3 | — | — |
| 48903 | `csherh1` / `csherh1` | Cảnh sát / quân đội / cứu hộ | 0,130 | 0,133 | 1.550 | 1.417 | 0,023 | 2 / 3 | — | — |
| 48904 | `dsherh1` / `dsherh1` | Cảnh sát / quân đội / cứu hộ | 0,130 | 0,133 | 1.550 | 1.417 | 0,023 | 2 / 3 | — | — |
| 48905 | `lapdh1` / `lapdh1` | Cảnh sát / quân đội / cứu hộ | 0,209 | 0,211 | 2.794 | 2.530 | 0,023 | 2 / 3 | — | — |
| 48906 | `lcpdh1` / `lcpdh1` | Cảnh sát / quân đội / cứu hộ | 0,131 | 0,133 | 1.562 | 1.420 | 0,023 | 2 / 4 | — | — |
| 48907 | `lvpdh1` / `lvpdh1` | Cảnh sát / quân đội / cứu hộ | 0,131 | 0,133 | 1.562 | 1.420 | 0,023 | 2 / 4 | — | — |
| 48908 | `mwpdh1` / `mwpdh1` | Cảnh sát / quân đội / cứu hộ | 0,126 | 0,129 | 1.556 | 1.322 | 0,023 | 2 / 3 | — | — |
| 48909 | `sfpdh1` / `sfpdh1` | Cảnh sát / quân đội / cứu hộ | 0,132 | 0,135 | 1.570 | 1.427 | 0,023 | 2 / 5 | — | Tên texture cần xác minh: sfpd1 |
| 48910 | `ulpdh1` / `ulpdh1` | Cảnh sát / quân đội / cứu hộ | 0,128 | 0,131 | 1.536 | 1.383 | 0,023 | 2 / 2 | — | — |
| 48911 | `vcpdh1` / `vcpdh1` | Cảnh sát / quân đội / cứu hộ | 0,131 | 0,133 | 1.562 | 1.420 | 0,023 | 2 / 4 | Vice City | — |
| 48912 | `ug_bp_bfybp` / `ug_bp_bfybp` | Dân thường | 0,134 | 0,137 | 1.387 | 1.393 | 0,031 | 2 / 3 | — | — |
| 48913 | `ug_bp_bmybp1` / `ug_bp_bmybp1` | Dân thường | 0,107 | 0,109 | 1.200 | 1.087 | 0,023 | 2 / 2 | — | — |
| 48914 | `ug_bp_bmybp2` / `ug_bp_bmybp2` | Dân thường | 0,107 | 0,109 | 1.200 | 1.087 | 0,023 | 2 / 2 | — | — |
| 48915 | `ug_bp_wfybp` / `ug_bp_wfybp` | Dân thường | 0,134 | 0,137 | 1.387 | 1.393 | 0,031 | 2 / 3 | — | — |
| 48916 | `ug_bp_wmybp2` / `ug_bp_wmybp2` | Dân thường | 0,108 | 0,109 | 1.218 | 1.154 | 0,021 | 1 / 1 | — | — |
| 48917 | `ug_bp_wmybp3` / `ug_bp_wmybp3` | Dân thường | 0,107 | 0,109 | 1.200 | 1.087 | 0,023 | 2 / 2 | — | — |
| 48918 | `AT_AAP1` / `AT_AAP1` | Gang | 0,098 | 0,100 | 1.150 | 1.079 | 0,016 | 1 / 2 | — | — |
| 48919 | `AT_AAP2` / `AT_AAP2` | Gang | 0,102 | 0,105 | 1.125 | 1.186 | 0,016 | 1 / 1 | — | — |
| 48920 | `AT_AAP3` / `AT_AAP3` | Gang | 0,089 | 0,092 | 1.101 | 930 | 0,016 | 1 / 1 | — | — |
| 48921 | `AT_ARMY` / `AT_ARMY` | Cảnh sát / quân đội / cứu hộ | 0,091 | 0,092 | 965 | 909 | 0,021 | 1 / 1 | — | — |
| 48922 | `AT_ATBURGSHOT` / `AT_ATBURGSHOT` | Dân thường | 0,171 | 0,174 | 2.086 | 1.677 | 0,042 | 1 / 1 | — | — |
| 48923 | `AT_ATMECH` / `AT_ATMECH` | Dân thường | 0,094 | 0,096 | 1.019 | 956 | 0,021 | 1 / 2 | — | — |
| 48924 | `AT_ATZ1` / `AT_ATZ1` | Gang | 0,115 | 0,117 | 1.258 | 1.168 | 0,026 | 2 / 2 | — | — |
| 48925 | `AT_ATZ2` / `AT_ATZ2` | Gang | 0,115 | 0,115 | 1.249 | 1.277 | 0,021 | 1 / 1 | — | — |
| 48926 | `AT_ATZ3` / `AT_ATZ3` | Gang | 0,124 | 0,125 | 1.502 | 1.369 | 0,021 | 1 / 1 | — | — |
| 48927 | `AT_BALLAS10` / `AT_BALLAS10` | Gang | 0,100 | 0,102 | 1.074 | 1.056 | 0,021 | 1 / 1 | — | — |
| 48928 | `AT_BALLAS11` / `AT_BALLAS11` | Gang | 0,110 | 0,111 | 1.156 | 1.123 | 0,025 | 2 / 3 | — | — |
| 48929 | `AT_BALLAS9` / `AT_BALLAS9` | Gang | 0,118 | 0,119 | 1.282 | 1.205 | 0,026 | 2 / 4 | — | — |
| 48930 | `AT_BFYBEAT` / `AT_BFYBEAT` | Dân thường | 0,107 | 0,109 | 1.242 | 1.134 | 0,021 | 1 / 1 | — | — |
| 48931 | `AT_BMYATBU` / `AT_BMYATBU` | Dân thường | 0,110 | 0,111 | 1.360 | 1.137 | 0,021 | 1 / 2 | — | — |
| 48932 | `AT_BMYBEAT` / `AT_BMYBEAT` | Dân thường | 0,090 | 0,092 | 1.140 | 820 | 0,021 | 1 / 2 | — | — |
| 48933 | `AT_BMYBEAT2` / `AT_BMYBEAT2` | Dân thường | 0,090 | 0,092 | 1.140 | 820 | 0,021 | 1 / 2 | — | — |
| 48934 | `AT_BMYDIFDH` / `AT_BMYDIFDH` | Dân thường | 0,132 | 0,135 | 1.208 | 1.108 | 0,047 | 2 / 3 | — | — |
| 48935 | `AT_BMYEMP` / `AT_BMYEMP` | Dân thường | 0,104 | 0,105 | 1.278 | 1.044 | 0,021 | 1 / 1 | — | — |
| 48936 | `AT_BMYFT` / `AT_BMYFT` | Dân thường | 0,097 | 0,098 | 1.181 | 942 | 0,021 | 1 / 2 | — | — |
| 48937 | `AT_BMYMOUN2` / `AT_BMYMOUN2` | Dân thường | 0,085 | 0,088 | 1.107 | 953 | 0,010 | 1 / 1 | — | — |
| 48938 | `AT_BMYPLT` / `AT_BMYPLT` | Dân thường | 0,090 | 0,092 | 990 | 884 | 0,021 | 1 / 1 | — | — |
| 48939 | `AT_BMYPSP` / `AT_BMYPSP` | Dân thường | 0,161 | 0,162 | 934 | 775 | 0,096 | 6 / 6 | — | — |
| 48940 | `AT_BMYRO` / `AT_BMYRO` | Dân thường | 0,091 | 0,094 | 1.157 | 937 | 0,016 | 1 / 2 | — | — |
| 48941 | `AT_CSHFYST` / `AT_CSHFYST` | Dân thường | 0,098 | 0,100 | 1.099 | 1.006 | 0,021 | 1 / 1 | — | — |
| 48942 | `AT_DNFYBE` / `AT_DNFYBE` | Dân thường | 0,118 | 0,121 | 1.231 | 1.129 | 0,031 | 2 / 2 | — | — |
| 48943 | `AT_FAM10` / `AT_FAM10` | Gang | 0,193 | 0,195 | 1.909 | 2.376 | 0,031 | 2 / 4 | — | — |
| 48944 | `AT_FAM11` / `AT_FAM11` | Gang | 0,098 | 0,102 | 1.173 | 1.072 | 0,016 | 1 / 2 | — | — |
| 48945 | `AT_FAM12` / `AT_FAM12` | Gang | 0,115 | 0,117 | 1.241 | 1.164 | 0,026 | 2 / 3 | — | — |
| 48946 | `AT_FBI` / `AT_FBI` | Cảnh sát / quân đội / cứu hộ | 0,090 | 0,092 | 1.037 | 864 | 0,021 | 1 / 1 | — | — |
| 48947 | `AT_FIREMAN` / `AT_FIREMAN` | Cảnh sát / quân đội / cứu hộ | 0,098 | 0,100 | 1.045 | 1.019 | 0,021 | 1 / 1 | — | — |
| 48948 | `AT_HBFYRI` / `AT_HBFYRI` | Dân thường | 0,121 | 0,123 | 1.236 | 1.411 | 0,021 | 1 / 3 | — | — |
| 48949 | `AT_HFYANT` / `AT_HFYANT` | Dân thường | 0,098 | 0,100 | 1.106 | 998 | 0,021 | 1 / 1 | — | — |
| 48950 | `AT_HFYBBU` / `AT_HFYBBU` | Dân thường | 0,116 | 0,117 | 1.208 | 1.322 | 0,021 | 1 / 1 | — | — |
| 48951 | `AT_HFYBE2` / `AT_HFYBE2` | Dân thường | 0,107 | 0,109 | 1.242 | 1.134 | 0,021 | 1 / 1 | — | — |
| 48952 | `AT_HFYLDSC` / `AT_HFYLDSC` | Dân thường | 0,141 | 0,143 | 1.382 | 1.253 | 0,046 | 2 / 2 | — | — |
| 48953 | `AT_HMYAP` / `AT_HMYAP` | Dân thường | 0,168 | 0,170 | 2.172 | 1.994 | 0,021 | 1 / 1 | — | — |
| 48954 | `AT_HMYMOUN2` / `AT_HMYMOUN2` | Dân thường | 0,085 | 0,088 | 1.107 | 953 | 0,010 | 1 / 1 | — | — |
| 48955 | `AT_HMYPBOX` / `AT_HMYPBOX` | Dân thường | 0,086 | 0,088 | 1.228 | 928 | 0,010 | 1 / 1 | — | — |
| 48956 | `AT_HMYTOUR` / `AT_HMYTOUR` | Dân thường | 0,098 | 0,100 | 1.084 | 968 | 0,022 | 2 / 3 | — | — |
| 48957 | `AT_MEDIATR` / `AT_MEDIATR` | Dân thường | 0,083 | 0,084 | 936 | 771 | 0,021 | 1 / 1 | — | — |
| 48958 | `AT_MEDIC` / `AT_MEDIC` | Cảnh sát / quân đội / cứu hộ | 0,090 | 0,092 | 1.024 | 865 | 0,021 | 1 / 1 | — | — |
| 48959 | `AT_OFYAV` / `AT_OFYAV` | Dân thường | 0,125 | 0,127 | 1.127 | 1.098 | 0,042 | 2 / 2 | — | — |
| 48960 | `AT_POLICE` / `AT_POLICE` | Cảnh sát / quân đội / cứu hộ | 0,129 | 0,131 | 1.671 | 1.407 | 0,021 | 1 / 1 | — | — |
| 48961 | `AT_SBATTR` / `AT_SBATTR` | Dân thường | 0,090 | 0,092 | 947 | 891 | 0,021 | 1 / 2 | — | — |
| 48962 | `AT_SBMYTR4` / `AT_SBMYTR4` | Dân thường | 0,181 | 0,184 | 856 | 677 | 0,125 | 1 / 1 | — | — |
| 48963 | `AT_SWAT` / `AT_SWAT` | Cảnh sát / quân đội / cứu hộ | 0,101 | 0,102 | 1.097 | 1.057 | 0,021 | 1 / 1 | — | — |
| 48964 | `AT_WFOBWB` / `AT_WFOBWB` | Dân thường | 0,089 | 0,090 | 1.098 | 822 | 0,021 | 1 / 1 | — | — |
| 48965 | `AT_WFOFU` / `AT_WFOFU` | Dân thường | 0,086 | 0,088 | 1.076 | 766 | 0,021 | 1 / 2 | — | — |
| 48966 | `AT_WFYBBU` / `AT_WFYBBU` | Dân thường | 0,104 | 0,105 | 1.089 | 1.127 | 0,021 | 1 / 1 | — | — |
| 48967 | `AT_WFYDJG` / `AT_WFYDJG` | Dân thường | 0,092 | 0,094 | 952 | 933 | 0,021 | 1 / 1 | — | — |
| 48968 | `AT_WFYDVJG` / `AT_WFYDVJG` | Dân thường | 0,095 | 0,096 | 999 | 974 | 0,021 | 1 / 1 | — | — |
| 48969 | `AT_WFYFBD` / `AT_WFYFBD` | Dân thường | 0,102 | 0,104 | 1.115 | 1.069 | 0,021 | 1 / 1 | — | — |
| 48970 | `AT_WFYFBE` / `AT_WFYFBE` | Dân thường | 0,076 | 0,078 | 876 | 652 | 0,021 | 1 / 1 | — | — |
| 48971 | `AT_WFYGPRO` / `AT_WFYGPRO` | Prostitute | 0,112 | 0,113 | 1.310 | 1.207 | 0,021 | 1 / 2 | — | — |
| 48972 | `AT_WFYJG1` / `AT_WFYJG1` | Dân thường | 0,106 | 0,107 | 1.091 | 1.154 | 0,021 | 1 / 3 | — | — |
| 48973 | `AT_WFYLPRO` / `AT_WFYLPRO` | Prostitute | 0,181 | 0,184 | 2.063 | 1.769 | 0,047 | 2 / 5 | — | — |
| 48974 | `AT_WFYLSGA` / `AT_WFYLSGA` | Dân thường | 0,085 | 0,086 | 940 | 803 | 0,021 | 1 / 1 | — | — |
| 48975 | `AT_WFYMYO` / `AT_WFYMYO` | Dân thường | 0,107 | 0,109 | 1.270 | 1.126 | 0,021 | 1 / 1 | — | — |
| 48976 | `AT_WFYOPRO` / `AT_WFYOPRO` | Prostitute | 0,112 | 0,113 | 1.310 | 1.207 | 0,021 | 1 / 2 | — | — |
| 48977 | `AT_WFYPLY` / `AT_WFYPLY` | Dân thường | 0,149 | 0,150 | 2.048 | 1.664 | 0,021 | 1 / 1 | — | — |
| 48978 | `AT_WFYRISX` / `AT_WFYRISX` | Dân thường | 0,099 | 0,102 | 1.091 | 1.047 | 0,020 | 2 / 3 | — | — |
| 48979 | `AT_WFYRO2` / `AT_WFYRO2` | Dân thường | 0,108 | 0,109 | 1.322 | 1.116 | 0,021 | 1 / 2 | — | — |
| 48980 | `AT_WFYRZH` / `AT_WFYRZH` | Prostitute | 0,111 | 0,113 | 1.179 | 1.232 | 0,021 | 1 / 1 | — | — |
| 48981 | `AT_WMOATBU` / `AT_WMOATBU` | Dân thường | 0,107 | 0,109 | 1.339 | 1.096 | 0,021 | 1 / 1 | — | — |
| 48982 | `AT_WMOTSH` / `AT_WMOTSH` | Dân thường | 0,089 | 0,090 | 1.047 | 840 | 0,021 | 1 / 1 | — | — |
| 48983 | `AT_WMYATBU` / `AT_WMYATBU` | Dân thường | 0,100 | 0,102 | 1.244 | 984 | 0,021 | 1 / 2 | — | — |
| 48984 | `AT_WMYATBU2` / `AT_WMYATBU2` | Dân thường | 0,100 | 0,102 | 1.244 | 984 | 0,021 | 1 / 2 | — | — |
| 48985 | `AT_WMYATBU3` / `AT_WMYATBU3` | Dân thường | 0,112 | 0,113 | 1.408 | 1.170 | 0,021 | 1 / 2 | — | — |
| 48986 | `AT_WMYBEAT` / `AT_WMYBEAT` | Dân thường | 0,087 | 0,090 | 1.140 | 875 | 0,016 | 1 / 1 | — | — |
| 48987 | `AT_WMYBEAT2` / `AT_WMYBEAT2` | Dân thường | 0,085 | 0,088 | 1.106 | 835 | 0,016 | 1 / 1 | — | — |
| 48988 | `AT_WMYBHC` / `AT_WMYBHC` | Criminal | 0,104 | 0,105 | 1.203 | 1.072 | 0,021 | 1 / 2 | — | — |
| 48989 | `AT_WMYBS` / `AT_WMYBS` | Dân thường | 0,110 | 0,111 | 1.241 | 1.183 | 0,021 | 1 / 1 | — | — |
| 48990 | `AT_WMYBS2` / `AT_WMYBS2` | Dân thường | 0,109 | 0,111 | 1.156 | 1.200 | 0,021 | 1 / 2 | — | — |
| 48991 | `AT_WMYBS3` / `AT_WMYBS3` | Dân thường | 0,106 | 0,107 | 1.147 | 1.151 | 0,021 | 1 / 1 | — | — |
| 48992 | `AT_WMYBS4` / `AT_WMYBS4` | Dân thường | 0,103 | 0,104 | 1.166 | 1.063 | 0,021 | 1 / 2 | — | — |
| 48993 | `AT_WMYCLX` / `AT_WMYCLX` | Dân thường | 0,088 | 0,090 | 1.006 | 833 | 0,021 | 1 / 1 | — | — |
| 48994 | `AT_WMYDTD` / `AT_WMYDTD` | Dân thường | 0,152 | 0,154 | 1.048 | 848 | 0,083 | 1 / 1 | — | — |
| 48995 | `AT_WMYEMP` / `AT_WMYEMP` | Dân thường | 0,082 | 0,084 | 882 | 768 | 0,021 | 1 / 1 | — | — |
| 48996 | `AT_WMYHIPST` / `AT_WMYHIPST` | Dân thường | 0,115 | 0,117 | 1.294 | 1.274 | 0,021 | 1 / 1 | — | — |
| 48997 | `AT_WMYJAN` / `AT_WMYJAN` | Dân thường | 0,167 | 0,168 | 2.128 | 1.573 | 0,042 | 1 / 1 | — | — |
| 48998 | `AT_WMYJCKT` / `AT_WMYJCKT` | Criminal | 0,084 | 0,086 | 936 | 789 | 0,021 | 1 / 1 | — | — |
| 48999 | `AT_WMYJG3` / `AT_WMYJG3` | Dân thường | 0,096 | 0,098 | 1.252 | 1.113 | 0,010 | 1 / 1 | — | — |
| 49000 | `AT_WMYLON` / `AT_WMYLON` | Dân thường | 0,115 | 0,117 | 985 | 960 | 0,042 | 1 / 1 | — | — |
| 49001 | `AT_WMYMIDGET` / `AT_WMYMIDGET` | Dân thường | 0,124 | 0,127 | 1.252 | 1.053 | 0,042 | 1 / 2 | — | — |
| 49002 | `AT_WMYMOUN3` / `AT_WMYMOUN3` | Dân thường | 0,085 | 0,088 | 1.107 | 953 | 0,010 | 1 / 1 | — | — |
| 49003 | `AT_WMYPREA` / `AT_WMYPREA` | Dân thường | 0,086 | 0,088 | 928 | 820 | 0,021 | 1 / 2 | — | — |
| 49004 | `AT_WMYPSP` / `AT_WMYPSP` | Dân thường | 0,171 | 0,172 | 1.020 | 946 | 0,096 | 6 / 6 | — | — |
| 49005 | `AT_WMYXCI` / `AT_WMYXCI` | Dân thường | 0,126 | 0,127 | 1.644 | 1.362 | 0,021 | 1 / 2 | — | — |
| 49006 | `AT_WMYZEN` / `AT_WMYZEN` | Dân thường | 0,100 | 0,102 | 1.122 | 1.034 | 0,021 | 1 / 1 | — | — |
| 49007 | `AT_WORK11` / `AT_WORK11` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49008 | `AT_WORK12` / `AT_WORK12` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49009 | `AT_WORK13` / `AT_WORK13` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49010 | `AT_WORK14` / `AT_WORK14` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49011 | `AT_WORK15` / `AT_WORK15` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49012 | `AT_WORK16` / `AT_WORK16` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49013 | `AT_WORK17` / `AT_WORK17` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49014 | `AT_WORK18` / `AT_WORK18` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49015 | `AT_WORK19` / `AT_WORK19` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49016 | `AT_WORK20` / `AT_WORK20` | Dân thường | 0,096 | 0,098 | 1.100 | 960 | 0,021 | 1 / 1 | — | — |
| 49017 | `AT_YC1` / `AT_YC1` | Gang | 0,101 | 0,102 | 1.060 | 1.079 | 0,021 | 1 / 1 | — | — |
| 49018 | `AT_YC2` / `AT_YC2` | Gang | 0,148 | 0,150 | 1.582 | 1.398 | 0,042 | 1 / 3 | — | — |
| 49019 | `AT_YC3` / `AT_YC3` | Gang | 0,129 | 0,131 | 1.705 | 1.396 | 0,021 | 1 / 1 | — | — |
| 49020 | `ARMYPILOT` / `ARMYPILOT` | Dân thường | 0,260 | 0,264 | 3.026 | 2.679 | 0,063 | 2 / 3 | — | — |
| 49021 | `ATNEWS` / `ATNEWS` | Dân thường | 0,128 | 0,129 | 1.427 | 1.301 | 0,029 | 3 / 4 | — | — |
| 49022 | `AT_BFYSK` / `AT_BFYSK` | Dân thường | 0,123 | 0,125 | 1.408 | 1.390 | 0,021 | 1 / 1 | — | — |
| 49023 | `AT_BFYSWAG` / `AT_BFYSWAG` | Dân thường | 0,170 | 0,172 | 1.799 | 1.755 | 0,042 | 1 / 1 | — | — |
| 49024 | `AT_WFYFYM` / `AT_WFYFYM` | Dân thường | 0,111 | 0,113 | 1.247 | 1.212 | 0,021 | 1 / 1 | — | — |
| 49025 | `AT_WFYHDG` / `AT_WFYHDG` | Dân thường | 0,108 | 0,109 | 1.226 | 1.152 | 0,021 | 1 / 1 | — | — |
| 49026 | `BWNEWS` / `BWNEWS` | Dân thường | 0,128 | 0,129 | 1.427 | 1.301 | 0,029 | 3 / 4 | — | — |
| 49027 | `CCNEWS` / `CCNEWS` | Dân thường | 0,128 | 0,129 | 1.427 | 1.301 | 0,029 | 3 / 4 | — | — |
| 49028 | `CMNEWS` / `CMNEWS` | Dân thường | 0,124 | 0,125 | 1.379 | 1.245 | 0,029 | 3 / 3 | — | — |
| 49029 | `DUN_GENERAL` / `DUN_GENERAL` | Dân thường | 0,237 | 0,238 | 2.667 | 2.565 | 0,052 | 2 / 3 | — | — |
| 49030 | `DUN_GUARD` / `DUN_GUARD` | Dân thường | 0,104 | 0,105 | 1.145 | 1.100 | 0,021 | 1 / 1 | — | — |
| 49031 | `DUN_RUN1` / `DUN_RUN1` | Dân thường | 0,101 | 0,102 | 1.205 | 1.017 | 0,021 | 1 / 1 | — | — |
| 49032 | `DUN_RUN2` / `DUN_RUN2` | Dân thường | 0,101 | 0,102 | 1.205 | 1.017 | 0,021 | 1 / 1 | — | — |
| 49033 | `DUN_RUN3` / `DUN_RUN3` | Dân thường | 0,102 | 0,104 | 1.265 | 1.024 | 0,021 | 1 / 2 | — | — |
| 49034 | `DUN_RUN4` / `DUN_RUN4` | Dân thường | 0,102 | 0,104 | 1.265 | 1.024 | 0,021 | 1 / 2 | — | — |
| 49035 | `DUN_SHIRT1` / `DUN_SHIRT1` | Dân thường | 0,169 | 0,170 | 1.646 | 2.229 | 0,021 | 1 / 1 | — | — |
| 49036 | `DUN_SHIRT2` / `DUN_SHIRT2` | Dân thường | 0,169 | 0,170 | 1.646 | 2.229 | 0,021 | 1 / 1 | — | — |
| 49037 | `DUN_SHIRT3` / `DUN_SHIRT3` | Dân thường | 0,168 | 0,170 | 1.598 | 2.230 | 0,021 | 1 / 1 | — | — |
| 49038 | `DUN_SHIRT4` / `DUN_SHIRT4` | Dân thường | 0,168 | 0,170 | 1.598 | 2.230 | 0,021 | 1 / 1 | — | — |
| 49039 | `DUN_SOLDIER1` / `DUN_SOLDIER1` | Dân thường | 0,091 | 0,092 | 970 | 909 | 0,021 | 1 / 1 | — | — |
| 49040 | `DUN_SOLDIER2` / `DUN_SOLDIER2` | Dân thường | 0,091 | 0,092 | 970 | 909 | 0,021 | 1 / 1 | — | — |
| 49041 | `DUN_WOMAN` / `DUN_WOMAN` | Dân thường | 0,112 | 0,113 | 1.304 | 1.188 | 0,021 | 1 / 4 | — | — |
| 49042 | `LCNEWS` / `LCNEWS` | Dân thường | 0,128 | 0,129 | 1.427 | 1.301 | 0,029 | 3 / 4 | — | — |
| 49043 | `MH2_BLOOD1` / `MH2_BLOOD1` | Dân thường | 0,224 | 0,225 | 1.914 | 1.961 | 0,083 | 2 / 2 | — | — |
| 49044 | `MH2_BLOOD2` / `MH2_BLOOD2` | Dân thường | 0,210 | 0,211 | 1.755 | 1.737 | 0,083 | 2 / 2 | — | — |
| 49045 | `MH2_BLOOD3` / `MH2_BLOOD3` | Dân thường | 0,218 | 0,219 | 1.872 | 1.861 | 0,083 | 2 / 2 | — | — |
| 49046 | `MH2_BLOOD4` / `MH2_BLOOD4` | Dân thường | 0,222 | 0,225 | 2.626 | 2.487 | 0,042 | 1 / 4 | — | — |
| 49047 | `MH2_BUM1` / `MH2_BUM1` | Dân thường | 0,194 | 0,195 | 2.044 | 1.936 | 0,052 | 2 / 2 | — | — |
| 49048 | `MH2_BUM2` / `MH2_BUM2` | Dân thường | 0,164 | 0,166 | 1.452 | 1.569 | 0,052 | 2 / 2 | — | — |
| 49049 | `MH2_BUMKINS1` / `MH2_BUMKINS1` | Dân thường | 0,197 | 0,199 | 1.981 | 2.021 | 0,052 | 2 / 3 | — | — |
| 49050 | `MH2_BUMKINS2` / `MH2_BUMKINS2` | Dân thường | 0,194 | 0,195 | 1.919 | 1.992 | 0,052 | 2 / 2 | — | — |
| 49051 | `MH2_BUMKINS3` / `MH2_BUMKINS3` | Dân thường | 0,194 | 0,195 | 2.009 | 1.942 | 0,052 | 2 / 2 | — | — |
| 49052 | `MH2_COP1` / `MH2_COP1` | Dân thường | 0,233 | 0,234 | 2.020 | 2.099 | 0,083 | 2 / 2 | — | — |
| 49053 | `MH2_COP2` / `MH2_COP2` | Dân thường | 0,202 | 0,203 | 2.036 | 2.105 | 0,052 | 2 / 2 | — | — |
| 49054 | `MH2_COPBIKER` / `MH2_COPBIKER` | Dân thường | 0,272 | 0,275 | 2.570 | 2.461 | 0,094 | 3 / 3 | — | — |
| 49055 | `MH2_DANNY` / `MH2_DANNY` | Dân thường | 0,250 | 0,252 | 2.410 | 2.294 | 0,083 | 2 / 3 | — | — |
| 49056 | `MH2_DANNY2` / `MH2_DANNY2` | Dân thường | 0,259 | 0,260 | 2.300 | 2.526 | 0,083 | 2 / 2 | — | — |
| 49057 | `MH2_DANNYBLOOD` / `MH2_DANNYBLOOD` | Dân thường | 0,250 | 0,252 | 2.410 | 2.294 | 0,083 | 2 / 3 | — | — |
| 49058 | `MH2_DOC` / `MH2_DOC` | Dân thường | 0,189 | 0,189 | 1.885 | 1.896 | 0,052 | 2 / 2 | — | — |
| 49059 | `MH2_DRWHITE` / `MH2_DRWHITE` | Dân thường | 0,189 | 0,189 | 1.882 | 1.891 | 0,052 | 2 / 2 | — | — |
| 49060 | `MH2_HOOKER1` / `MH2_HOOKER1` | Prostitute | 0,178 | 0,180 | 1.856 | 1.688 | 0,052 | 2 / 2 | — | — |
| 49061 | `MH2_HOOKER2` / `MH2_HOOKER2` | Prostitute | 0,209 | 0,211 | 1.856 | 1.688 | 0,083 | 2 / 2 | — | — |
| 49062 | `MH2_HOOKER3` / `MH2_HOOKER3` | Prostitute | 0,174 | 0,176 | 1.896 | 1.581 | 0,052 | 2 / 2 | — | — |
| 49063 | `MH2_INSANE1` / `MH2_INSANE1` | Dân thường | 0,189 | 0,189 | 1.886 | 1.889 | 0,052 | 2 / 2 | — | — |
| 49064 | `MH2_INSANE2` / `MH2_INSANE2` | Dân thường | 0,189 | 0,189 | 1.892 | 1.888 | 0,052 | 2 / 2 | — | — |
| 49065 | `MH2_JOHNA` / `MH2_JOHNA` | Dân thường | 0,212 | 0,213 | 1.898 | 1.735 | 0,083 | 2 / 2 | — | — |
| 49066 | `MH2_JOHNB` / `MH2_JOHNB` | Dân thường | 0,212 | 0,213 | 1.848 | 1.751 | 0,083 | 2 / 2 | — | — |
| 49067 | `MH2_JUDY` / `MH2_JUDY` | Dân thường | 0,228 | 0,229 | 2.075 | 1.983 | 0,083 | 2 / 2 | — | — |
| 49068 | `MH2_LEG1` / `MH2_LEG1` | Dân thường | 0,209 | 0,209 | 1.998 | 2.249 | 0,052 | 2 / 2 | — | — |
| 49069 | `MH2_LEG2` / `MH2_LEG2` | Dân thường | 0,240 | 0,242 | 2.000 | 2.255 | 0,083 | 2 / 2 | — | — |
| 49070 | `MH2_LEG3` / `MH2_LEG3` | Dân thường | 0,212 | 0,213 | 1.968 | 2.338 | 0,052 | 2 / 2 | — | — |
| 49071 | `MH2_LEO` / `MH2_LEO` | Dân thường | 0,239 | 0,240 | 2.250 | 2.142 | 0,083 | 2 / 2 | — | — |
| 49072 | `MH2_LEO2` / `MH2_LEO2` | Dân thường | 0,237 | 0,238 | 2.098 | 2.140 | 0,083 | 2 / 3 | — | — |
| 49073 | `MH2_LEOBLOODY` / `MH2_LEOBLOODY` | Dân thường | 0,237 | 0,238 | 2.098 | 2.140 | 0,083 | 2 / 3 | — | — |
| 49074 | `MH2_MECH1` / `MH2_MECH1` | Dân thường | 0,180 | 0,182 | 1.848 | 1.727 | 0,052 | 2 / 2 | — | — |
| 49075 | `MH2_MECH2` / `MH2_MECH2` | Dân thường | 0,181 | 0,184 | 1.910 | 1.734 | 0,052 | 2 / 2 | — | — |
| 49076 | `MH2_MICHAEL` / `MH2_MICHAEL` | Dân thường | 0,223 | 0,225 | 2.022 | 1.896 | 0,083 | 2 / 2 | — | — |
| 49077 | `MH2_ORD1` / `MH2_ORD1` | Dân thường | 0,222 | 0,223 | 1.895 | 1.922 | 0,083 | 2 / 2 | — | — |
| 49078 | `MH2_ORD2` / `MH2_ORD2` | Dân thường | 0,222 | 0,223 | 1.883 | 1.924 | 0,083 | 2 / 2 | — | — |
| 49079 | `MH2_ORD3` / `MH2_ORD3` | Dân thường | 0,217 | 0,219 | 1.847 | 1.853 | 0,083 | 2 / 2 | — | — |
| 49080 | `MH2_PARAMEDIC` / `MH2_PARAMEDIC` | Dân thường | 0,185 | 0,186 | 1.730 | 1.873 | 0,052 | 2 / 2 | — | — |
| 49081 | `MH2_PERV1` / `MH2_PERV1` | Dân thường | 0,228 | 0,229 | 2.005 | 1.998 | 0,083 | 2 / 2 | — | — |
| 49082 | `MH2_PERV2` / `MH2_PERV2` | Dân thường | 0,225 | 0,227 | 1.872 | 1.989 | 0,083 | 2 / 2 | — | — |
| 49083 | `MH2_PERV3` / `MH2_PERV3` | Dân thường | 0,210 | 0,211 | 1.720 | 1.757 | 0,083 | 2 / 2 | — | — |
| 49084 | `MH2_PERV4` / `MH2_PERV4` | Dân thường | 0,200 | 0,201 | 1.686 | 1.575 | 0,083 | 2 / 2 | — | — |
| 49085 | `MH2_PERV5` / `MH2_PERV5` | Dân thường | 0,211 | 0,213 | 1.834 | 1.723 | 0,083 | 2 / 3 | — | — |
| 49086 | `MH2_PERV6` / `MH2_PERV6` | Dân thường | 0,202 | 0,203 | 1.676 | 1.604 | 0,083 | 2 / 2 | — | — |
| 49087 | `MH2_PERVCAT` / `MH2_PERVCAT` | Dân thường | 0,240 | 0,240 | 2.221 | 2.164 | 0,083 | 2 / 2 | — | — |
| 49088 | `MH2_PERVGIMP` / `MH2_PERVGIMP` | Dân thường | 0,233 | 0,234 | 2.002 | 2.096 | 0,083 | 2 / 3 | — | — |
| 49089 | `MH2_PERVHORSE` / `MH2_PERVHORSE` | Dân thường | 0,362 | 0,363 | 2.084 | 2.159 | 0,208 | 2 / 2 | — | — |
| 49090 | `MH2_PERVJANITOR` / `MH2_PERVJANITOR` | Dân thường | 0,212 | 0,213 | 1.884 | 1.736 | 0,083 | 2 / 2 | — | — |
| 49091 | `MH2_PERVPIGGSY` / `MH2_PERVPIGGSY` | Dân thường | 0,228 | 0,229 | 2.012 | 2.000 | 0,083 | 2 / 2 | — | — |
| 49092 | `MH2_PERVPISS` / `MH2_PERVPISS` | Dân thường | 0,234 | 0,234 | 1.984 | 2.130 | 0,083 | 2 / 3 | — | — |
| 49093 | `MH2_PERVUNICORN` / `MH2_PERVUNICORN` | Dân thường | 0,366 | 0,367 | 2.154 | 2.209 | 0,208 | 2 / 2 | — | — |
| 49094 | `MH2_PERVVAMP` / `MH2_PERVVAMP` | Dân thường | 0,245 | 0,246 | 2.217 | 2.277 | 0,083 | 2 / 2 | — | — |
| 49095 | `MH2_PICKMAN` / `MH2_PICKMAN` | Dân thường | 0,239 | 0,240 | 2.130 | 2.190 | 0,083 | 2 / 2 | — | — |
| 49096 | `MH2_PM1` / `MH2_PM1` | Dân thường | 0,226 | 0,227 | 2.002 | 1.962 | 0,083 | 2 / 2 | — | — |
| 49097 | `MH2_PM2` / `MH2_PM2` | Dân thường | 0,226 | 0,227 | 1.992 | 1.968 | 0,083 | 2 / 2 | — | — |
| 49098 | `MH2_PM3` / `MH2_PM3` | Dân thường | 0,230 | 0,230 | 2.058 | 2.028 | 0,083 | 2 / 2 | — | — |
| 49099 | `MH2_PM4` / `MH2_PM4` | Dân thường | 0,233 | 0,234 | 2.074 | 2.074 | 0,083 | 2 / 2 | — | — |
| 49100 | `MH2_RK1` / `MH2_RK1` | Dân thường | 0,208 | 0,209 | 1.850 | 1.667 | 0,083 | 2 / 2 | — | — |
| 49101 | `MH2_RK2` / `MH2_RK2` | Dân thường | 0,229 | 0,230 | 1.848 | 2.085 | 0,083 | 2 / 2 | — | — |
| 49102 | `MH2_RK3` / `MH2_RK3` | Dân thường | 0,206 | 0,207 | 1.808 | 1.643 | 0,083 | 2 / 2 | — | — |
| 49103 | `MH2_RK4` / `MH2_RK4` | Dân thường | 0,208 | 0,209 | 1.820 | 1.667 | 0,083 | 2 / 2 | — | — |
| 49104 | `MH2_SCARECROW` / `MH2_SCARECROW` | Dân thường | 0,531 | 0,533 | 3.408 | 8.202 | 0,052 | 2 / 5 | — | — |
| 49105 | `MH2_SLP` / `MH2_SLP` | Dân thường | 0,179 | 0,182 | 1.826 | 1.727 | 0,052 | 2 / 2 | — | — |
| 49106 | `MH2_SLP2` / `MH2_SLP2` | Dân thường | 0,189 | 0,189 | 1.968 | 1.858 | 0,052 | 2 / 2 | — | — |
| 49107 | `MH2_SLP3` / `MH2_SLP3` | Dân thường | 0,183 | 0,186 | 1.868 | 1.792 | 0,052 | 2 / 2 | — | — |
| 49108 | `MH2_SURGEON` / `MH2_SURGEON` | Dân thường | 0,253 | 0,254 | 2.214 | 2.440 | 0,083 | 2 / 2 | — | — |
| 49109 | `MH2_SWAT1` / `MH2_SWAT1` | Dân thường | 0,241 | 0,242 | 2.096 | 2.224 | 0,083 | 2 / 2 | — | — |
| 49110 | `MH2_SWAT2` / `MH2_SWAT2` | Dân thường | 0,261 | 0,262 | 2.292 | 2.557 | 0,083 | 2 / 3 | — | — |
| 49111 | `MH2_SWAT3` / `MH2_SWAT3` | Dân thường | 0,245 | 0,246 | 2.160 | 2.294 | 0,083 | 2 / 3 | — | — |
| 49112 | `MH2_SWAT4` / `MH2_SWAT4` | Dân thường | 0,244 | 0,244 | 2.148 | 2.262 | 0,083 | 2 / 3 | — | — |
| 49113 | `MH2_VICTIM` / `MH2_VICTIM` | Dân thường | 0,163 | 0,164 | 1.678 | 1.455 | 0,052 | 2 / 2 | — | — |
| 49114 | `MH2_WATCHDOGS1` / `MH2_WATCHDOGS1` | Dân thường | 0,193 | 0,195 | 1.962 | 1.952 | 0,052 | 2 / 2 | — | — |
| 49115 | `MH2_WATCHDOGS2` / `MH2_WATCHDOGS2` | Dân thường | 0,220 | 0,221 | 1.900 | 1.884 | 0,083 | 2 / 2 | — | — |
| 49116 | `MH2_WATCHDOGS3` / `MH2_WATCHDOGS3` | Dân thường | 0,235 | 0,236 | 2.032 | 2.144 | 0,083 | 2 / 2 | — | — |
| 49117 | `MH2_WATCHDOGS4` / `MH2_WATCHDOGS4` | Dân thường | 0,225 | 0,227 | 1.942 | 1.976 | 0,083 | 2 / 2 | — | — |
| 49118 | `MH2_WATCHDOGS5` / `MH2_WATCHDOGS5` | Dân thường | 0,229 | 0,230 | 1.992 | 2.036 | 0,083 | 2 / 2 | — | — |
| 49119 | `MH2_WATCHDOGS6` / `MH2_WATCHDOGS6` | Dân thường | 0,231 | 0,232 | 2.028 | 2.059 | 0,083 | 2 / 2 | — | — |
| 49120 | `MH2_WIFE` / `MH2_WIFE` | Dân thường | 0,229 | 0,230 | 2.068 | 1.998 | 0,083 | 2 / 2 | — | — |
| 49121 | `MWNEWS` / `MWNEWS` | Dân thường | 0,128 | 0,129 | 1.427 | 1.301 | 0,029 | 3 / 4 | — | — |
| 49122 | `SANEWS` / `SANEWS` | Dân thường | 0,124 | 0,125 | 1.379 | 1.245 | 0,029 | 3 / 3 | — | — |
| 49123 | `ULNEWS` / `ULNEWS` | Dân thường | 0,160 | 0,162 | 1.379 | 1.245 | 0,065 | 3 / 3 | — | — |
| 49124 | `UL_AMMUGUY` / `UL_AMMUGUY` | Dân thường | 0,178 | 0,180 | 2.148 | 1.786 | 0,042 | 1 / 1 | — | — |
| 49125 | `UL_BFYDANC` / `UL_BFYDANC` | Dân thường | 0,139 | 0,141 | 1.706 | 1.491 | 0,026 | 2 / 2 | — | — |
| 49126 | `UL_BFYKPRO` / `UL_BFYKPRO` | Prostitute | 0,125 | 0,127 | 1.344 | 1.022 | 0,042 | 1 / 2 | — | — |
| 49127 | `UL_BFYMECH` / `UL_BFYMECH` | Dân thường | 0,116 | 0,119 | 1.174 | 1.114 | 0,031 | 2 / 4 | — | — |
| 49128 | `UL_BFYNG` / `UL_BFYNG` | Dân thường | 0,262 | 0,264 | 1.206 | 1.322 | 0,167 | 1 / 1 | — | — |
| 49129 | `UL_BFYNRD` / `UL_BFYNRD` | Dân thường | 0,247 | 0,250 | 1.107 | 1.064 | 0,167 | 1 / 1 | — | — |
| 49130 | `UL_BFYOTH` / `UL_BFYOTH` | Dân thường | 0,252 | 0,254 | 1.165 | 1.147 | 0,167 | 1 / 1 | — | — |
| 49131 | `UL_BFYQP` / `UL_BFYQP` | Dân thường | 0,289 | 0,291 | 1.054 | 1.298 | 0,198 | 2 / 1 | — | — |
| 49132 | `UL_BMYBALL` / `UL_BMYBALL` | Dân thường | 0,107 | 0,107 | 1.167 | 1.152 | 0,021 | 1 / 1 | — | — |
| 49133 | `UL_BMYCPP` / `UL_BMYCPP` | Dân thường | 0,095 | 0,096 | 1.087 | 937 | 0,021 | 1 / 2 | — | — |
| 49134 | `UL_BMYCS` / `UL_BMYCS` | Dân thường | 0,246 | 0,248 | 1.095 | 1.037 | 0,167 | 1 / 1 | — | — |
| 49135 | `UL_BMYEME` / `UL_BMYEME` | Dân thường | 0,147 | 0,148 | 1.618 | 1.254 | 0,047 | 2 / 2 | — | — |
| 49136 | `UL_BMYFDP` / `UL_BMYFDP` | Dân thường | 0,098 | 0,100 | 1.156 | 977 | 0,021 | 1 / 2 | — | — |
| 49137 | `UL_BMYMECH` / `UL_BMYMECH` | Dân thường | 0,178 | 0,180 | 2.214 | 1.954 | 0,031 | 2 / 6 | — | Tên texture cần xác minh: sweet |
| 49138 | `UL_BMYOB` / `UL_BMYOB` | Dân thường | 0,110 | 0,111 | 1.246 | 962 | 0,031 | 2 / 2 | — | — |
| 49139 | `UL_BMYSG` / `UL_BMYSG` | Criminal | 0,096 | 0,098 | 1.112 | 948 | 0,021 | 1 / 1 | — | — |
| 49140 | `UL_DNMYLCL` / `UL_DNMYLCL` | Dân thường | 0,089 | 0,090 | 1.002 | 848 | 0,021 | 1 / 1 | — | — |
| 49141 | `UL_FBI` / `UL_FBI` | Cảnh sát / quân đội / cứu hộ | 0,085 | 0,086 | 952 | 788 | 0,021 | 1 / 1 | — | — |
| 49142 | `UL_HFOCWS` / `UL_HFOCWS` | Dân thường | 0,229 | 0,230 | 1.014 | 739 | 0,167 | 1 / 1 | — | — |
| 49143 | `UL_HFOTN` / `UL_HFOTN` | Dân thường | 0,232 | 0,234 | 1.002 | 791 | 0,167 | 1 / 1 | — | — |
| 49144 | `UL_HFYGRPRO` / `UL_HFYGRPRO` | Prostitute | 0,092 | 0,094 | 1.048 | 901 | 0,021 | 1 / 2 | — | — |
| 49145 | `UL_HFYHBS` / `UL_HFYHBS` | Dân thường | 0,226 | 0,229 | 932 | 709 | 0,167 | 1 / 1 | — | — |
| 49146 | `UL_HFYRWA` / `UL_HFYRWA` | Dân thường | 0,113 | 0,115 | 1.151 | 1.284 | 0,021 | 1 / 1 | — | — |
| 49147 | `UL_HFYSMG` / `UL_HFYSMG` | Dân thường | 0,252 | 0,254 | 1.144 | 1.156 | 0,167 | 1 / 1 | — | — |
| 49148 | `UL_HFYUFM` / `UL_HFYUFM` | Dân thường | 0,256 | 0,258 | 1.284 | 1.176 | 0,167 | 1 / 1 | — | — |
| 49149 | `UL_HMOFM` / `UL_HMOFM` | Dân thường | 0,240 | 0,242 | 1.090 | 928 | 0,167 | 1 / 1 | — | — |
| 49150 | `UL_HMOHOBO` / `UL_HMOHOBO` | Dân thường | 0,233 | 0,236 | 950 | 846 | 0,167 | 1 / 1 | — | — |
| 49151 | `UL_HMYENBU` / `UL_HMYENBU` | Dân thường | 0,090 | 0,092 | 962 | 898 | 0,021 | 1 / 2 | — | — |
| 49152 | `UL_HUNTER1` / `UL_HUNTER1` | Dân thường | 0,108 | 0,109 | 1.318 | 1.125 | 0,021 | 1 / 1 | — | — |
| 49153 | `UL_HUNTER2` / `UL_HUNTER2` | Dân thường | 0,165 | 0,168 | 2.115 | 1.735 | 0,031 | 2 / 4 | — | — |
| 49154 | `UL_HUNTER3` / `UL_HUNTER3` | Dân thường | 0,105 | 0,107 | 1.164 | 1.121 | 0,021 | 1 / 1 | — | — |
| 49155 | `UL_OFOHW` / `UL_OFOHW` | Dân thường | 0,231 | 0,234 | 1.050 | 771 | 0,167 | 1 / 1 | — | — |
| 49156 | `UL_OFYBG` / `UL_OFYBG` | Dân thường | 0,133 | 0,135 | 1.035 | 1.304 | 0,042 | 2 / 2 | — | — |
| 49157 | `UL_OFYFMC` / `UL_OFYFMC` | Dân thường | 0,248 | 0,250 | 1.086 | 1.084 | 0,167 | 1 / 1 | — | — |
| 49158 | `UL_OMYPSP` / `UL_OMYPSP` | Dân thường | 0,169 | 0,170 | 1.039 | 904 | 0,096 | 6 / 6 | — | — |
| 49159 | `UL_OMYRCBU` / `UL_OMYRCBU` | Dân thường | 0,120 | 0,123 | 1.127 | 1.228 | 0,031 | 1 / 1 | — | — |
| 49160 | `UL_POLICE` / `UL_POLICE` | Cảnh sát / quân đội / cứu hộ | 0,416 | 0,418 | 3.628 | 3.509 | 0,167 | 1 / 1 | — | — |
| 49161 | `UL_RICHCB` / `UL_RICHCB` | Dân thường | 0,125 | 0,127 | 1.194 | 875 | 0,052 | 2 / 2 | — | — |
| 49162 | `UL_RN1` / `UL_RN1` | Dân thường | 0,082 | 0,084 | 978 | 716 | 0,021 | 1 / 2 | — | — |
| 49163 | `UL_RN2` / `UL_RN2` | Dân thường | 0,085 | 0,086 | 965 | 783 | 0,021 | 1 / 1 | — | — |
| 49164 | `UL_RN3` / `UL_RN3` | Dân thường | 0,083 | 0,084 | 992 | 749 | 0,021 | 1 / 1 | — | — |
| 49165 | `UL_TEXAN1` / `UL_TEXAN1` | Dân thường | 0,103 | 0,104 | 1.086 | 1.103 | 0,021 | 1 / 1 | — | — |
| 49166 | `UL_TEXAN2` / `UL_TEXAN2` | Dân thường | 0,103 | 0,104 | 1.086 | 1.103 | 0,021 | 1 / 1 | — | — |
| 49167 | `UL_TEXAN3` / `UL_TEXAN3` | Dân thường | 0,121 | 0,123 | 1.142 | 1.014 | 0,042 | 2 / 3 | — | — |
| 49168 | `UL_WFOAP` / `UL_WFOAP` | Dân thường | 0,237 | 0,238 | 1.051 | 872 | 0,167 | 1 / 2 | — | — |
| 49169 | `UL_WFOCF` / `UL_WFOCF` | Dân thường | 0,089 | 0,090 | 1.026 | 838 | 0,021 | 1 / 2 | — | — |
| 49170 | `UL_WFOHBB` / `UL_WFOHBB` | Dân thường | 0,233 | 0,234 | 942 | 840 | 0,167 | 1 / 1 | — | — |
| 49171 | `UL_WFOLC` / `UL_WFOLC` | Dân thường | 0,086 | 0,088 | 944 | 810 | 0,021 | 1 / 1 | — | — |
| 49172 | `UL_WFOMG` / `UL_WFOMG` | Dân thường | 0,228 | 0,230 | 996 | 724 | 0,167 | 1 / 1 | — | — |
| 49173 | `UL_WFOWM` / `UL_WFOWM` | Dân thường | 0,232 | 0,234 | 889 | 844 | 0,167 | 1 / 1 | — | — |
| 49174 | `UL_WFYBBC` / `UL_WFYBBC` | Dân thường | 0,235 | 0,236 | 958 | 879 | 0,167 | 1 / 1 | — | — |
| 49175 | `UL_WFYBGF` / `UL_WFYBGF` | Dân thường | 0,085 | 0,086 | 1.006 | 765 | 0,021 | 1 / 1 | — | — |
| 49176 | `UL_WFYBSF` / `UL_WFYBSF` | Dân thường | 0,090 | 0,092 | 1.040 | 863 | 0,021 | 1 / 1 | — | — |
| 49177 | `UL_WFYCPV` / `UL_WFYCPV` | Dân thường | 0,250 | 0,252 | 1.153 | 1.101 | 0,167 | 1 / 1 | — | — |
| 49178 | `UL_WFYFCY` / `UL_WFYFCY` | Dân thường | 0,103 | 0,104 | 1.188 | 1.062 | 0,021 | 1 / 1 | — | — |
| 49179 | `UL_WFYFLASHPRO` / `UL_WFYFLASHPRO` | Prostitute | 0,187 | 0,189 | 2.269 | 2.120 | 0,031 | 2 / 2 | — | — |
| 49180 | `UL_WFYLUXPRO` / `UL_WFYLUXPRO` | Prostitute | 0,088 | 0,090 | 1.104 | 797 | 0,021 | 1 / 2 | — | — |
| 49181 | `UL_WFYMCPRO` / `UL_WFYMCPRO` | Prostitute | 0,266 | 0,268 | 1.252 | 1.396 | 0,167 | 1 / 1 | — | — |
| 49182 | `UL_WFYNLH` / `UL_WFYNLH` | Dân thường | 0,231 | 0,232 | 954 | 795 | 0,167 | 1 / 1 | — | — |
| 49183 | `UL_WFYOTW` / `UL_WFYOTW` | Dân thường | 0,234 | 0,236 | 985 | 839 | 0,167 | 1 / 1 | — | — |
| 49184 | `UL_WFYRDN` / `UL_WFYRDN` | Dân thường | 0,180 | 0,182 | 1.190 | 932 | 0,104 | 2 / 4 | — | — |
| 49185 | `UL_WFYSXC` / `UL_WFYSXC` | Dân thường | 0,235 | 0,236 | 971 | 865 | 0,167 | 1 / 1 | — | — |
| 49186 | `UL_WFYTSP` / `UL_WFYTSP` | Dân thường | 0,086 | 0,088 | 996 | 805 | 0,021 | 1 / 1 | — | — |
| 49187 | `UL_WMOFAZ` / `UL_WMOFAZ` | Dân thường | 0,082 | 0,084 | 911 | 747 | 0,021 | 1 / 1 | — | — |
| 49188 | `UL_WMOHBA` / `UL_WMOHBA` | Dân thường | 0,143 | 0,145 | 1.588 | 1.297 | 0,042 | 1 / 1 | — | — |
| 49189 | `UL_WMOHBGP` / `UL_WMOHBGP` | Dân thường | 0,087 | 0,088 | 1.035 | 787 | 0,021 | 1 / 3 | — | — |
| 49190 | `UL_WMOPL` / `UL_WMOPL` | Dân thường | 0,128 | 0,129 | 1.414 | 1.052 | 0,042 | 1 / 2 | — | — |
| 49191 | `UL_WMORFM` / `UL_WMORFM` | Dân thường | 0,089 | 0,090 | 999 | 855 | 0,021 | 1 / 2 | — | — |
| 49192 | `UL_WMOSNOW` / `UL_WMOSNOW` | Dân thường | 0,084 | 0,086 | 1.032 | 750 | 0,021 | 1 / 1 | — | — |
| 49193 | `UL_WMOSTG` / `UL_WMOSTG` | Dân thường | 0,121 | 0,123 | 1.555 | 1.284 | 0,021 | 1 / 2 | — | — |
| 49194 | `UL_WMOWBU` / `UL_WMOWBU` | Dân thường | 0,097 | 0,098 | 1.060 | 986 | 0,021 | 1 / 1 | — | — |
| 49195 | `UL_WMYAGC` / `UL_WMYAGC` | Dân thường | 0,092 | 0,094 | 1.089 | 876 | 0,021 | 1 / 2 | — | — |
| 49196 | `UL_WMYBCB` / `UL_WMYBCB` | Dân thường | 0,087 | 0,088 | 995 | 820 | 0,021 | 1 / 1 | — | — |
| 49197 | `UL_WMYCV` / `UL_WMYCV` | Dân thường | 0,088 | 0,090 | 1.004 | 828 | 0,021 | 1 / 1 | — | — |
| 49198 | `UL_WMYGHC` / `UL_WMYGHC` | Dân thường | 0,104 | 0,105 | 1.203 | 1.072 | 0,021 | 1 / 2 | — | — |
| 49199 | `UL_WMYGM` / `UL_WMYGM` | Dân thường | 0,129 | 0,131 | 1.765 | 1.363 | 0,021 | 1 / 1 | — | — |
| 49200 | `UL_WMYGOR` / `UL_WMYGOR` | Dân thường | 0,092 | 0,094 | 998 | 907 | 0,021 | 1 / 2 | — | — |
| 49201 | `UL_WMYHP` / `UL_WMYHP` | Criminal | 0,121 | 0,123 | 1.297 | 1.325 | 0,023 | 2 / 2 | — | — |
| 49202 | `UL_WMYHWSCB` / `UL_WMYHWSCB` | Dân thường | 0,083 | 0,084 | 978 | 748 | 0,021 | 1 / 1 | — | — |
| 49203 | `UL_WMYJK` / `UL_WMYJK` | Dân thường | 0,108 | 0,111 | 1.116 | 988 | 0,031 | 2 / 2 | — | — |
| 49204 | `UL_WMYMECH` / `UL_WMYMECH` | Dân thường | 0,254 | 0,256 | 1.211 | 1.168 | 0,167 | 1 / 1 | — | — |
| 49205 | `UL_WMYOSG` / `UL_WMYOSG` | Dân thường | 0,223 | 0,225 | 850 | 674 | 0,167 | 1 / 1 | — | — |
| 49206 | `UL_WMYRATFM` / `UL_WMYRATFM` | Dân thường | 0,103 | 0,104 | 1.167 | 1.072 | 0,021 | 1 / 1 | — | — |
| 49207 | `UL_WMYSAF` / `UL_WMYSAF` | Dân thường | 0,089 | 0,090 | 929 | 883 | 0,021 | 1 / 2 | — | — |
| 49208 | `UL_WMYSMD` / `UL_WMYSMD` | Dân thường | 0,239 | 0,240 | 994 | 936 | 0,167 | 1 / 1 | — | — |
| 49209 | `UL_WMYSMPRO` / `UL_WMYSMPRO` | Prostitute | 0,091 | 0,092 | 1.034 | 877 | 0,021 | 1 / 2 | — | — |
| 49210 | `UL_WMYSOS` / `UL_WMYSOS` | Dân thường | 0,130 | 0,133 | 1.458 | 1.087 | 0,042 | 1 / 2 | — | — |
| 49211 | `UL_WMYVDBD` / `UL_WMYVDBD` | Dân thường | 0,093 | 0,094 | 1.048 | 914 | 0,021 | 1 / 2 | — | — |
| 49212 | `VCNEWS` / `VCNEWS` | Dân thường | 0,124 | 0,125 | 1.379 | 1.245 | 0,029 | 3 / 3 | Vice City | — |
| 49213 | `CC_CCSWAT2` / `CC_CCSWAT2` | Cảnh sát / quân đội / cứu hộ | 0,174 | 0,176 | 1.252 | 1.210 | 0,083 | 2 / 2 | — | — |
| 49214 | `LCS_CAMP_MAN` / `LCS_CAMP_MAN` | Dân thường | 0,118 | 0,119 | 1.115 | 1.614 | 0,008 | 9 / 9 | — | — |
| 49215 | `LCS_CAMP_WOM` / `LCS_CAMP_WOM` | Dân thường | 0,108 | 0,109 | 1.006 | 1.460 | 0,008 | 7 / 7 | — | — |
| 49216 | `LCS_COP` / `LCS_COP` | Cảnh sát / quân đội / cứu hộ | 0,094 | 0,096 | 889 | 1.258 | 0,006 | 7 / 7 | — | — |
| 49217 | `LCS_FBI` / `LCS_FBI` | Cảnh sát / quân đội / cứu hộ | 0,105 | 0,105 | 933 | 1.389 | 0,009 | 9 / 11 | — | — |
| 49218 | `LCS_MEDIC` / `LCS_MEDIC` | Cảnh sát / quân đội / cứu hộ | 0,117 | 0,119 | 1.142 | 1.604 | 0,007 | 7 / 7 | — | — |
| 49219 | `LCS_SWAT` / `LCS_SWAT` | Cảnh sát / quân đội / cứu hộ | 0,099 | 0,102 | 920 | 1.357 | 0,005 | 9 / 10 | — | — |
| 49220 | `LCS_ARMY` / `LCS_ARMY` | Cảnh sát / quân đội / cứu hộ | 0,117 | 0,119 | 1.102 | 1.639 | 0,006 | 7 / 8 | — | — |
| 49221 | `LCS_B_MAN1` / `LCS_B_MAN1` | Dân thường | 0,100 | 0,104 | 921 | 1.355 | 0,007 | 7 / 7 | — | — |
| 49222 | `LCS_B_MAN2` / `LCS_B_MAN2` | Dân thường | 0,125 | 0,127 | 1.200 | 1.699 | 0,009 | 7 / 7 | — | — |
| 49223 | `LCS_B_MAN3` / `LCS_B_MAN3` | Dân thường | 0,108 | 0,109 | 1.040 | 1.499 | 0,006 | 5 / 6 | — | — |
| 49224 | `LCS_B_WOM1` / `LCS_B_WOM1` | Dân thường | 0,098 | 0,100 | 898 | 1.328 | 0,006 | 8 / 9 | — | — |
| 49225 | `LCS_B_WOM2` / `LCS_B_WOM2` | Dân thường | 0,107 | 0,109 | 1.024 | 1.479 | 0,007 | 5 / 6 | — | — |
| 49226 | `LCS_BABY` / `LCS_BABY` | Dân thường | 0,138 | 0,141 | 1.229 | 1.739 | 0,019 | 9 / 10 | — | — |
| 49227 | `LCS_BUGFOUND` / `LCS_BUGFOUND` | Dân thường | 0,083 | 0,084 | 772 | 1.165 | 0,003 | 3 / 3 | — | — |
| 49228 | `LCS_CAS_MAN` / `LCS_CAS_MAN` | Dân thường | 0,123 | 0,125 | 1.212 | 1.741 | 0,006 | 5 / 5 | — | — |
| 49229 | `LCS_CHAUFF` / `LCS_CHAUFF` | Dân thường | 0,133 | 0,137 | 1.258 | 1.816 | 0,011 | 5 / 5 | — | — |
| 49230 | `LCS_EIGHT` / `LCS_EIGHT` | Dân thường | 0,124 | 0,127 | 1.160 | 1.688 | 0,009 | 7 / 7 | — | — |
| 49231 | `LCS_GRDANG3` / `LCS_GRDANG3` | Gang | 0,089 | 0,090 | 998 | 1.031 | 0,010 | 8 / 8 | — | — |
| 49232 | `LCS_GREASE` / `LCS_GREASE` | Dân thường | 0,110 | 0,111 | 934 | 1.356 | 0,017 | 6 / 6 | — | — |
| 49233 | `LCS_HITMAN` / `LCS_HITMAN` | Dân thường | 0,200 | 0,201 | 1.935 | 2.709 | 0,020 | 6 / 6 | — | — |
| 49234 | `LCS_HOODS01` / `LCS_HOODS01` | Gang | 0,171 | 0,174 | 1.678 | 2.447 | 0,009 | 7 / 7 | — | — |
| 49235 | `LCS_HOODS02` / `LCS_HOODS02` | Gang | 0,177 | 0,180 | 1.750 | 2.530 | 0,009 | 8 / 8 | — | — |
| 49236 | `LCS_JDMADE` / `LCS_CHAUFF` | Dân thường | 0,162 | 0,166 | 1.548 | 2.307 | 0,011 | 5 / 2 | — | Tên texture cần xác minh: ig_otoole_head,ig_otoole_suit |
| 49237 | `LCS_TONI1` / `LCS_TONI1` | Model có pedtype PLAYER1/2 | 0,209 | 0,211 | 1.800 | 2.600 | 0,039 | 2 / 2 | — | — |
| 49238 | `LCS_TONI2` / `LCS_TONI2` | Model có pedtype PLAYER1/2 | 0,225 | 0,227 | 1.960 | 2.849 | 0,039 | 2 / 2 | — | — |
| 49239 | `LCS_TONI3` / `LCS_TONI3` | Model có pedtype PLAYER1/2 | 0,209 | 0,211 | 1.800 | 2.600 | 0,039 | 2 / 2 | — | — |
| 49240 | `LCS_TONI4` / `LCS_TONI4` | Model có pedtype PLAYER1/2 | 0,232 | 0,234 | 2.290 | 3.301 | 0,017 | 5 / 5 | — | — |
| 49241 | `LCS_TONI5` / `LCS_TONI5` | Model có pedtype PLAYER1/2 | 0,214 | 0,215 | 2.004 | 2.846 | 0,026 | 6 / 7 | — | — |
| 49242 | `LCS_TONI6` / `LCS_TONI6` | Model có pedtype PLAYER1/2 | 0,264 | 0,264 | 2.345 | 3.437 | 0,040 | 7 / 7 | — | — |
| 49243 | `LCS_TONI7` / `LCS_TONI7` | Model có pedtype PLAYER1/2 | 0,202 | 0,203 | 1.832 | 2.668 | 0,026 | 7 / 7 | — | — |
| 49244 | `LCS_TONI8` / `LCS_TONI8` | Model có pedtype PLAYER1/2 | 0,223 | 0,227 | 2.124 | 3.056 | 0,023 | 7 / 7 | — | — |
| 49245 | `LCS_TONI9` / `LCS_TONI9` | Model có pedtype PLAYER1/2 | 0,129 | 0,131 | 1.132 | 1.717 | 0,013 | 9 / 9 | — | — |
| 49246 | `LCS_TONI10` / `LCS_TONI10` | Model có pedtype PLAYER1/2 | 0,205 | 0,207 | 1.916 | 2.717 | 0,025 | 6 / 6 | — | — |
| 49247 | `LCS_TONI11` / `LCS_TONI11` | Model có pedtype PLAYER1/2 | 0,214 | 0,215 | 1.916 | 2.718 | 0,034 | 8 / 8 | — | — |
| 49248 | `LCS_TONI12` / `LCS_TONI12` | Model có pedtype PLAYER1/2 | 0,202 | 0,205 | 1.854 | 2.647 | 0,027 | 6 / 6 | — | — |
| 49249 | `LCS_TONI13` / `LCS_TONI13` | Model có pedtype PLAYER1/2 | 0,200 | 0,201 | 1.826 | 2.596 | 0,028 | 6 / 6 | — | — |
| 49250 | `LCS_TONI14` / `LCS_TONI14` | Model có pedtype PLAYER1/2 | 0,214 | 0,215 | 1.920 | 2.834 | 0,028 | 6 / 6 | — | — |
| 49251 | `LCS_TONI15` / `LCS_TONI15` | Model có pedtype PLAYER1/2 | 0,204 | 0,205 | 1.846 | 2.628 | 0,030 | 7 / 7 | — | — |
| 49252 | `LCS_TONI16` / `LCS_TONI16` | Model có pedtype PLAYER1/2 | 0,199 | 0,201 | 1.858 | 2.688 | 0,022 | 6 / 6 | — | — |
| 49253 | `LCS_TONIBETA1` / `LCS_TONIBETA1` | Model có pedtype PLAYER1/2 | 0,192 | 0,193 | 1.566 | 2.450 | 0,031 | 9 / 16 | — | — |
| 49254 | `LCS_TONIBETA2` / `LCS_TONIBETA2` | Model có pedtype PLAYER1/2 | 0,183 | 0,184 | 1.713 | 2.581 | 0,015 | 6 / 6 | — | — |
| 49255 | `LCS_TONIBETA3` / `LCS_TONIBETA3` | Model có pedtype PLAYER1/2 | 0,206 | 0,207 | 1.860 | 2.743 | 0,026 | 7 / 7 | — | — |
| 49256 | `LCS_TONIBETA4` / `LCS_TONIBETA4` | Model có pedtype PLAYER1/2 | 0,203 | 0,205 | 1.838 | 2.617 | 0,030 | 7 / 7 | — | — |
| 49257 | `LCS_TRIAD1` / `LCS_TRIAD1` | Gang | 0,126 | 0,127 | 1.190 | 1.694 | 0,010 | 10 / 10 | — | — |
| 49258 | `LCS_TRIAD2` / `LCS_TRIAD2` | Gang | 0,117 | 0,119 | 1.112 | 1.591 | 0,008 | 8 / 8 | — | — |
| 49259 | `LCS_YARDIE01` / `LCS_YARDIE01` | Gang | 0,103 | 0,104 | 928 | 1.370 | 0,009 | 7 / 7 | — | — |
| 49260 | `LCS_YARDIE02` / `LCS_YARDIE02` | Gang | 0,106 | 0,107 | 946 | 1.428 | 0,009 | 9 / 9 | — | — |
| 49261 | `LCS_YARDIE03` / `LCS_YARDIE03` | Gang | 0,118 | 0,121 | 969 | 1.515 | 0,015 | 6 / 11 | — | — |
| 49262 | `LCS_B_WOM3` / `LCS_B_WOM3` | Dân thường | 0,106 | 0,107 | 982 | 1.457 | 0,008 | 2 / 2 | — | — |
| 49263 | `LCS_WKAS` / `LCS_WKAS` | Dân thường | 0,219 | 0,221 | 2.182 | 3.049 | 0,018 | 7 / 7 | — | — |
| 49264 | `LCS_CASA` / `LCS_CASA` | Dân thường | 0,144 | 0,146 | 1.261 | 1.777 | 0,024 | 7 / 8 | — | — |
| 49265 | `LC_MARIA` / `LC_MARIA` | Dân thường | 0,535 | 0,537 | 4.680 | 6.170 | 0,133 | 2 / 4 | — | — |
| 49266 | `LC_NOVY` / `LC_NOVY` | Dân thường | 0,102 | 0,105 | 1.018 | 910 | 0,031 | 1 / 1 | — | — |
| 49267 | `LC_BUTLER` / `LC_BUTLER` | Dân thường | 0,218 | 0,221 | 2.848 | 2.366 | 0,039 | 2 / 4 | — | — |
| 49268 | `LC_COP2` / `LC_COP2` | Cảnh sát / quân đội / cứu hộ | 0,113 | 0,115 | 1.478 | 1.417 | 0,008 | 1 / 2 | — | — |
| 49269 | `LC_DARKEL` / `LC_DARKEL` | Dân thường | 0,077 | 0,080 | 969 | 863 | 0,008 | 4 / 6 | — | — |
| 49270 | `LC_DONKY` / `LC_DONKY` | Dân thường | 0,088 | 0,092 | 966 | 1.094 | 0,008 | 1 / 9 | — | — |
| 49271 | `UG_WMYRPLT` / `UG_WMYRPLT` | Dân thường | 0,151 | 0,154 | 1.452 | 1.880 | 0,023 | 2 / 3 | — | — |
| 49272 | `SA_BALLAS10` / `SA_BALLAS10` | Gang | 0,106 | 0,109 | 1.265 | 1.122 | 0,020 | 2 / 4 | Carcer City, Los Santos | — |
| 49273 | `SA_TRIADC` / `SA_TRIADC` | Gang | 0,147 | 0,148 | 1.728 | 1.334 | 0,042 | 1 / 1 | Carcer City, Los Santos | — |
| 49274 | `SA_TRIADELDER` / `SA_TRIADELDER` | Gang | 0,103 | 0,105 | 1.069 | 1.119 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 49275 | `SA_VLA4` / `SA_VLA4` | Gang | 0,108 | 0,109 | 1.258 | 1.148 | 0,021 | 1 / 1 | Carcer City, Los Santos | — |
| 49276 | `SA_VLA5` / `SA_VLA5` | Gang | 0,115 | 0,117 | 1.313 | 1.366 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 49277 | `SA_VLA6` / `SA_VLA6` | Gang | 0,108 | 0,111 | 1.267 | 1.227 | 0,016 | 1 / 6 | Carcer City, Los Santos | — |
| 49278 | `LC_BUSKER1` / `LC_BUSKER1` | Dân thường | 0,090 | 0,094 | 1.043 | 1.101 | 0,008 | 1 / 10 | — | — |
| 49279 | `LC_BUSKER2` / `LC_BUSKER2` | Dân thường | 0,092 | 0,096 | 1.071 | 1.158 | 0,008 | 1 / 1 | — | — |
| 49280 | `LC_BUSKER3` / `LC_BUSKER3` | Dân thường | 0,066 | 0,068 | 731 | 718 | 0,008 | 1 / 12 | — | — |
| 49281 | `LC_BUSKER4` / `LC_BUSKER4` | Dân thường | 0,079 | 0,082 | 933 | 918 | 0,008 | 1 / 11 | — | — |
| 49282 | `VC_UMBERTO` / `VC_UMBERTO` | Dân thường | 0,157 | 0,160 | 2.164 | 1.568 | 0,031 | 1 / 1 | — | — |
| 49283 | `VC_VICTOR` / `VC_VICTOR` | Dân thường | 0,189 | 0,191 | 2.380 | 1.925 | 0,042 | 1 / 1 | — | — |
| 49284 | `VC_ASS1` / `VC_ASS1` | Dân thường | 0,107 | 0,109 | 1.098 | 983 | 0,031 | 1 / 1 | — | — |
| 49285 | `VC_ASS2` / `VC_ASS2` | Dân thường | 0,107 | 0,109 | 1.098 | 983 | 0,031 | 1 / 1 | — | — |
| 49286 | `VC_ASS3` / `VC_ASS3` | Dân thường | 0,107 | 0,109 | 1.098 | 983 | 0,031 | 1 / 1 | — | — |
| 49287 | `VC_BJ` / `VC_BJ` | Dân thường | 0,188 | 0,191 | 2.404 | 2.103 | 0,031 | 1 / 1 | — | — |
| 49288 | `VC_CANDY` / `VC_CANDY` | Prostitute | 0,180 | 0,182 | 2.472 | 1.913 | 0,031 | 1 / 1 | — | — |
| 49289 | `VC_CGOON01` / `VC_CGOON01` | Gang | 0,117 | 0,119 | 1.186 | 1.137 | 0,031 | 1 / 1 | — | — |
| 49290 | `VC_CGOON02` / `VC_CGOON02` | Gang | 0,117 | 0,119 | 1.186 | 1.137 | 0,031 | 1 / 1 | — | — |
| 49291 | `VC_CGOON03` / `VC_CGOON03` | Gang | 0,117 | 0,119 | 1.186 | 1.137 | 0,031 | 1 / 1 | — | — |
| 49292 | `VC_COURIER` / `VC_COURIER` | Dân thường | 0,097 | 0,100 | 1.044 | 1.111 | 0,016 | 1 / 1 | — | — |
| 49293 | `VC_DGOON2` / `VC_DGOON2` | Gang | 0,103 | 0,105 | 1.174 | 863 | 0,031 | 1 / 1 | — | — |
| 49294 | `VC_DIAZ` / `VC_DIAZ` | Dân thường | 0,172 | 0,176 | 2.279 | 1.834 | 0,031 | 1 / 1 | — | — |
| 49295 | `VC_DICK` / `VC_DICK` | Dân thường | 0,171 | 0,174 | 2.008 | 1.906 | 0,031 | 1 / 1 | — | — |
| 49296 | `VC_DIRECTOR` / `VC_DIRECTOR` | Dân thường | 0,200 | 0,203 | 2.718 | 2.226 | 0,031 | 1 / 1 | — | — |
| 49297 | `VC_DLOVE` / `VC_DLOVE` | Dân thường | 0,164 | 0,166 | 2.019 | 1.769 | 0,031 | 1 / 1 | — | — |
| 49298 | `VC_DORIS` / `VC_DORIS` | Dân thường | 0,184 | 0,188 | 2.488 | 1.994 | 0,031 | 1 / 1 | — | — |
| 49299 | `VC_DWAYNE` / `VC_DWAYNE` | Dân thường | 0,169 | 0,172 | 2.282 | 1.776 | 0,031 | 1 / 1 | — | — |
| 49300 | `VC_GONZALEZ` / `VC_GONZALEZ` | Dân thường | 0,178 | 0,180 | 2.115 | 1.812 | 0,042 | 1 / 1 | — | — |
| 49301 | `VC_HILARY` / `VC_HILARY` | Dân thường | 0,173 | 0,176 | 2.436 | 1.798 | 0,031 | 1 / 1 | — | — |
| 49302 | `VC_HILARY2` / `VC_HILARY2` | Dân thường | 0,119 | 0,121 | 1.030 | 1.029 | 0,042 | 1 / 1 | — | — |
| 49303 | `VC_JETHRO` / `VC_JETHRO` | Dân thường | 0,172 | 0,174 | 2.276 | 1.829 | 0,031 | 1 / 1 | — | — |
| 49304 | `VC_JEZZ` / `VC_JEZZ` | Dân thường | 0,182 | 0,184 | 2.283 | 2.024 | 0,031 | 1 / 1 | — | — |
| 49305 | `VC_JUGGZ` / `VC_JUGGZ` | Dân thường | 0,100 | 0,102 | 1.288 | 1.067 | 0,016 | 1 / 1 | — | — |
| 49306 | `VC_JZGIRL` / `VC_JZGIRL` | Dân thường | 0,069 | 0,072 | 830 | 628 | 0,016 | 1 / 1 | — | — |
| 49307 | `VC_KELLY` / `VC_KELLY` | Dân thường | 0,204 | 0,207 | 2.598 | 2.351 | 0,031 | 1 / 1 | — | — |
| 49308 | `VC_KEN` / `VC_KEN` | Dân thường | 0,217 | 0,219 | 2.856 | 2.507 | 0,031 | 1 / 1 | — | — |
| 49309 | `VC_LANCE` / `VC_LANCE` | Dân thường | 0,194 | 0,197 | 2.372 | 2.038 | 0,042 | 1 / 1 | — | — |
| 49310 | `VC_LANCE2` / `VC_LANCE2` | Dân thường | 0,149 | 0,152 | 1.805 | 1.543 | 0,031 | 1 / 2 | — | — |
| 49311 | `VC_LANCE3` / `VC_LANCE3` | Dân thường | 0,184 | 0,188 | 2.372 | 2.038 | 0,031 | 1 / 1 | — | — |
| 49312 | `VC_MAUDE` / `VC_MAUDE` | Dân thường | 0,181 | 0,184 | 2.255 | 2.020 | 0,031 | 1 / 1 | — | — |
| 49313 | `VC_MERCEDES` / `VC_MERCEDES` | Dân thường | 0,172 | 0,176 | 2.326 | 1.819 | 0,031 | 1 / 1 | — | — |
| 49314 | `VC_MERCEDES2` / `VC_MERCEDES2` | Dân thường | 0,152 | 0,154 | 2.000 | 1.526 | 0,031 | 1 / 1 | — | — |
| 49315 | `VC_MGOONA` / `VC_MGOONA` | Dân thường | 0,093 | 0,096 | 997 | 1.054 | 0,016 | 1 / 1 | — | — |
| 49316 | `VC_MIKE` / `VC_MIKE` | Dân thường | 0,170 | 0,172 | 2.238 | 1.803 | 0,031 | 1 / 1 | — | — |
| 49317 | `VC_MIKE2` / `VC_MIKE2` | Dân thường | 0,144 | 0,146 | 1.530 | 1.341 | 0,042 | 1 / 1 | — | — |
| 49318 | `VC_MITCH` / `VC_MITCH` | Dân thường | 0,168 | 0,170 | 2.230 | 1.766 | 0,031 | 1 / 1 | — | — |
| 49319 | `VC_PAPA` / `VC_PAPA` | Dân thường | 0,128 | 0,129 | 1.244 | 1.122 | 0,042 | 1 / 1 | — | — |
| 49320 | `VC_PERCY` / `VC_PERCY` | Dân thường | 0,175 | 0,178 | 2.135 | 1.940 | 0,031 | 1 / 2 | — | — |
| 49321 | `VC_PHIL` / `VC_PHIL` | Dân thường | 0,178 | 0,182 | 2.324 | 1.934 | 0,031 | 1 / 1 | — | — |
| 49322 | `VC_PHIL2` / `VC_PHIL2` | Dân thường | 0,167 | 0,170 | 2.151 | 1.786 | 0,031 | 1 / 1 | — | — |
| 49323 | `VC_PHIL3` / `VC_PHIL3` | Dân thường | 0,117 | 0,119 | 1.016 | 996 | 0,042 | 1 / 1 | — | — |
| 49324 | `VC_RICHARDS` / `VC_RICHARDS` | Dân thường | 0,141 | 0,145 | 1.713 | 1.420 | 0,031 | 1 / 1 | — | — |
| 49325 | `VC_SERV` / `VC_SERV` | Dân thường | 0,078 | 0,080 | 963 | 761 | 0,016 | 1 / 1 | — | — |
| 49326 | `VC_SHRUB` / `VC_SHRUB` | Dân thường | 0,170 | 0,172 | 2.236 | 1.801 | 0,031 | 1 / 1 | — | — |
| 49327 | `VC_SHRUB2` / `VC_SHRUB2` | Dân thường | 0,143 | 0,146 | 1.956 | 1.378 | 0,031 | 1 / 1 | — | — |
| 49328 | `VC_SONNY` / `VC_SONNY` | Dân thường | 0,179 | 0,182 | 2.504 | 1.888 | 0,031 | 1 / 1 | — | — |
| 49329 | `AT_WMYRCK` / `AT_WMYRCK` | Dân thường | 0,124 | 0,125 | 1.454 | 1.392 | 0,021 | 1 / 1 | — | — |
| 49330 | `CC_AMMUCLERK` / `CC_AMMUCLERK` | Dân thường | 0,159 | 0,162 | 1.284 | 1.104 | 0,073 | 2 / 3 | — | — |
| 49331 | `SA_BDUP` / `SA_BDUP` | Dân thường | 0,156 | 0,158 | 2.053 | 1.594 | 0,031 | 1 / 1 | — | — |
| 49332 | `SA_BETTINA` / `SA_BETTINA` | Dân thường | 0,155 | 0,158 | 1.978 | 1.612 | 0,031 | 1 / 1 | — | — |
| 49333 | `SA_BMYDJB` / `SA_BMYDJB` | Dân thường | 0,095 | 0,098 | 1.121 | 1.037 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 49334 | `SA_BOGMAN` / `SA_BOGMAN` | Dân thường | 0,155 | 0,158 | 2.122 | 1.552 | 0,031 | 1 / 1 | — | — |
| 49335 | `SA_BURGER` / `SA_BURGER` | Dân thường | 0,161 | 0,164 | 2.086 | 1.677 | 0,031 | 1 / 1 | — | — |
| 49336 | `SA_CDEPUT` / `SA_CDEPUT` | Cảnh sát / quân đội / cứu hộ | 0,189 | 0,191 | 928 | 801 | 0,125 | 1 / 1 | — | — |
| 49337 | `SA_CSMECH` / `SA_CSMECH` | Dân thường | 0,090 | 0,092 | 1.022 | 967 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 49338 | `SA_DANCEA` / `SA_DANCEA` | Dân thường | 0,102 | 0,105 | 1.104 | 1.187 | 0,016 | 1 / 1 | — | — |
| 49339 | `SA_DANCEB` / `SA_DANCEB` | Dân thường | 0,102 | 0,105 | 1.104 | 1.187 | 0,016 | 1 / 1 | — | — |
| 49340 | `SA_DRUG1` / `SA_DRUG1` | Criminal | 0,094 | 0,098 | 1.095 | 1.030 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 49341 | `SA_FARLIE` / `SA_FARLIE` | Dân thường | 0,138 | 0,141 | 1.647 | 1.377 | 0,031 | 1 / 2 | — | — |
| 49342 | `SA_HELPER1` / `SA_HELPER1` | Dân thường | 0,130 | 0,133 | 1.788 | 1.478 | 0,016 | 1 / 1 | — | — |
| 49343 | `SA_HELPER2` / `SA_HELPER2` | Dân thường | 0,130 | 0,133 | 1.788 | 1.478 | 0,016 | 1 / 1 | — | — |
| 49344 | `SA_HO` / `SA_HO` | Prostitute | 0,076 | 0,078 | 970 | 705 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 49345 | `SA_JOSE` / `SA_JOSE` | Dân thường | 0,165 | 0,168 | 2.238 | 1.713 | 0,031 | 1 / 1 | — | — |
| 49346 | `SA_LAPDM1B` / `SA_LAPDM1B` | Cảnh sát / quân đội / cứu hộ | 0,093 | 0,096 | 1.026 | 1.034 | 0,016 | 1 / 1 | — | — |
| 49347 | `SA_LILBILL` / `SA_LILBILL` | Dân thường | 0,140 | 0,143 | 1.678 | 1.418 | 0,031 | 1 / 1 | — | — |
| 49348 | `SA_MAFGOON1` / `SA_MAFGOON1` | Dân thường | 0,121 | 0,125 | 1.722 | 1.342 | 0,016 | 1 / 1 | — | — |
| 49349 | `SA_MAFGOON2` / `SA_MAFGOON2` | Dân thường | 0,123 | 0,127 | 1.768 | 1.360 | 0,016 | 1 / 1 | — | — |
| 49350 | `SA_MARIA` / `SA_MARIA` | Dân thường | 0,160 | 0,162 | 2.032 | 1.680 | 0,031 | 1 / 1 | — | — |
| 49351 | `SA_MEDIATR` / `SA_MEDIATR` | Dân thường | 0,188 | 0,191 | 936 | 785 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 49352 | `SA_OGLOCBURGER` / `SA_OGLOCBURGER` | Dân thường | 0,156 | 0,160 | 2.067 | 1.600 | 0,031 | 1 / 1 | — | — |
| 49353 | `SA_PENDELBURY` / `SA_PENDELBURY` | Dân thường | 0,087 | 0,090 | 1.044 | 900 | 0,016 | 1 / 1 | — | — |
| 49354 | `SA_PLAS1` / `SA_PLAS1` | Dân thường | 0,162 | 0,164 | 2.114 | 1.696 | 0,031 | 1 / 1 | — | — |
| 49355 | `SA_POOLGUY` / `SA_POOLGUY` | Dân thường | 0,122 | 0,125 | 1.458 | 1.131 | 0,031 | 1 / 1 | — | — |
| 49356 | `SA_PRO1` / `SA_PRO1` | Prostitute | 0,078 | 0,080 | 966 | 754 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 49357 | `SA_PSYCHO` / `SA_PSYCHO` | Dân thường | 0,182 | 0,186 | 860 | 688 | 0,125 | 1 / 1 | — | — |
| 49358 | `SA_SALVATORE` / `SA_SALVATORE` | Dân thường | 0,161 | 0,164 | 2.112 | 1.670 | 0,031 | 1 / 1 | — | — |
| 49359 | `SA_SBMYTR4` / `SA_SBMYTR4` | Dân thường | 0,181 | 0,184 | 856 | 677 | 0,125 | 1 / 1 | Carcer City, Los Santos | — |
| 49360 | `SA_SILVERMAN` / `SA_SILVERMAN` | Dân thường | 0,161 | 0,164 | 2.160 | 1.664 | 0,031 | 1 / 1 | — | — |
| 49361 | `SA_SINDACCOGOON` / `SA_SINDACCOGOON` | Dân thường | 0,157 | 0,160 | 2.124 | 1.597 | 0,031 | 1 / 1 | — | — |
| 49362 | `SA_SLUT` / `SA_SLUT` | Dân thường | 0,158 | 0,160 | 2.108 | 1.619 | 0,031 | 1 / 1 | — | — |
| 49363 | `SA_SMOKEV2` / `SA_SMOKEV2` | Dân thường | 0,138 | 0,141 | 1.615 | 1.404 | 0,031 | 1 / 1 | — | — |
| 49364 | `SA_SUIT2` / `SA_SUIT2` | Dân thường | 0,079 | 0,082 | 912 | 798 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 49365 | `SA_WMYBP2` / `SA_WMYBP2` | Dân thường | 0,104 | 0,107 | 1.218 | 1.179 | 0,016 | 1 / 1 | Carcer City, Los Santos | — |
| 49366 | `SA_WMYCD2` / `SA_WMYCD2` | Dân thường | 0,189 | 0,191 | 940 | 808 | 0,125 | 1 / 1 | — | — |
| 49367 | `ULPDM1` / `ULPDM1` | Cảnh sát / quân đội / cứu hộ | 0,123 | 0,125 | 1.463 | 1.371 | 0,021 | 1 / 1 | — | — |
| 49368 | `VCS_BARRY` / `VCS_BARRY` | Dân thường | 0,151 | 0,152 | 1.146 | 1.706 | 0,036 | 9 / 9 | — | — |
| 49369 | `VCS_CSPED1` / `VCS_CSPED1` | Dân thường | 0,234 | 0,236 | 2.013 | 2.949 | 0,041 | 8 / 8 | — | — |
| 49370 | `VCS_DASS1` / `VCS_DASS1` | Dân thường | 0,111 | 0,113 | 1.002 | 1.500 | 0,009 | 7 / 7 | Vice City | — |
| 49371 | `VCS_DASS2` / `VCS_DASS2` | Dân thường | 0,074 | 0,076 | 1.016 | 758 | 0,009 | 7 / 7 | Vice City | — |
| 49372 | `VCS_DASS3` / `VCS_DASS3` | Dân thường | 0,232 | 0,234 | 1.996 | 3.029 | 0,035 | 8 / 8 | Vice City | — |
| 49373 | `VCS_DASS4` / `VCS_DASS4` | Dân thường | 0,250 | 0,252 | 1.882 | 2.877 | 0,063 | 8 / 8 | Vice City | Đuôi nonzero DFF |
| 49374 | `VCS_FORBES1` / `VCS_FORBES1` | Dân thường | 0,142 | 0,145 | 1.043 | 1.543 | 0,037 | 8 / 8 | — | — |
| 49375 | `VCS_FORBES2` / `VCS_FORBES2` | Dân thường | 0,143 | 0,145 | 1.053 | 1.539 | 0,038 | 9 / 9 | — | — |
| 49376 | `VCS_FORBES3` / `VCS_FORBES3` | Dân thường | 0,146 | 0,146 | 1.113 | 1.695 | 0,032 | 7 / 7 | — | — |
| 49377 | `VCS_FRANK` / `VCS_FRANK` | Dân thường | 0,256 | 0,258 | 2.254 | 3.214 | 0,045 | 10 / 9 | — | — |
| 49378 | `VCS_GANG9A` / `VCS_GANG9A` | Dân thường | 0,116 | 0,119 | 1.048 | 1.537 | 0,011 | 10 / 10 | — | — |
| 49379 | `VCS_GANG9B` / `VCS_GANG9B` | Dân thường | 0,112 | 0,113 | 1.022 | 1.482 | 0,009 | 10 / 11 | — | — |
| 49380 | `VCS_GONZALEZ` / `VCS_GONZALEZ` | Dân thường | 0,074 | 0,076 | 983 | 703 | 0,012 | 8 / 8 | — | — |
| 49381 | `VCS_HANK` / `VCS_HANK` | Dân thường | 0,218 | 0,221 | 1.884 | 2.868 | 0,031 | 8 / 8 | — | — |
| 49382 | `VCS_JANET` / `VCS_JANET` | Dân thường | 0,230 | 0,232 | 1.922 | 2.778 | 0,047 | 8 / 8 | — | — |
| 49383 | `VCS_JAVIER` / `VCS_JAVIER` | Dân thường | 0,210 | 0,211 | 1.928 | 2.789 | 0,026 | 9 / 9 | — | — |
| 49384 | `VCS_LANCE1` / `VCS_LANCE1` | Dân thường | 0,141 | 0,143 | 1.176 | 1.657 | 0,028 | 7 / 7 | — | — |
| 49385 | `VCS_LANCE2` / `VCS_LANCE2` | Dân thường | 0,162 | 0,164 | 1.242 | 1.837 | 0,038 | 8 / 8 | — | — |
| 49386 | `VCS_LOUISE1` / `VCS_LOUISE1` | Dân thường | 0,162 | 0,164 | 1.298 | 1.908 | 0,033 | 8 / 8 | — | — |
| 49387 | `VCS_LOUISE2` / `VCS_LOUISE2` | Dân thường | 0,265 | 0,266 | 2.296 | 3.402 | 0,043 | 10 / 10 | — | — |
| 49388 | `VCS_LOUISE3` / `VCS_LOUISE3` | Dân thường | 0,166 | 0,168 | 1.282 | 1.915 | 0,038 | 9 / 10 | — | — |
| 49389 | `VCS_LOUISE4` / `VCS_LOUISE4` | Dân thường | 0,147 | 0,148 | 1.282 | 1.930 | 0,018 | 10 / 11 | — | — |
| 49390 | `VCS_MARTY` / `VCS_MARTY` | Dân thường | 0,142 | 0,145 | 1.066 | 1.583 | 0,035 | 8 / 8 | — | — |
| 49391 | `VCS_MARYJ` / `VCS_MARYJ` | Dân thường | 0,227 | 0,230 | 1.930 | 2.774 | 0,044 | 7 / 7 | — | — |
| 49392 | `VCS_PHILC2` / `VCS_PHILC2` | Dân thường | 0,164 | 0,166 | 1.326 | 1.960 | 0,033 | 7 / 7 | — | — |
| 49393 | `VCS_PINATA` / `VCS_PINATA` | Dân thường | 0,074 | 0,076 | 708 | 992 | 0,004 | 5 / 5 | — | — |
| 49394 | `VCS_RENI` / `VCS_RENI` | Dân thường | 0,155 | 0,158 | 1.214 | 1.794 | 0,034 | 8 / 8 | — | — |
| 49395 | `VCS_RENIOP` / `VCS_RENIOP` | Dân thường | 0,167 | 0,170 | 1.350 | 2.010 | 0,033 | 9 / 9 | — | — |
| 49396 | `VCS_TROY` / `VCS_TROY` | Dân thường | 0,237 | 0,238 | 2.068 | 3.075 | 0,035 | 10 / 10 | — | — |
| 49397 | `VCS_UMBERTO` / `VCS_UMBERTO` | Dân thường | 0,168 | 0,170 | 1.438 | 2.022 | 0,031 | 8 / 8 | — | — |
| 49398 | `VCS_VIC1` / `VCS_VIC1` | Dân thường | 0,222 | 0,225 | 1.644 | 2.376 | 0,065 | 8 / 8 | — | — |
| 49399 | `VCS_VIC10` / `VCS_VIC10` | Dân thường | 0,204 | 0,205 | 1.658 | 2.468 | 0,042 | 6 / 6 | — | — |
| 49400 | `VCS_VIC11` / `VCS_VIC11` | Dân thường | 0,191 | 0,191 | 1.614 | 2.336 | 0,036 | 6 / 6 | — | — |
| 49401 | `VCS_VIC12` / `VCS_VIC12` | Dân thường | 0,183 | 0,186 | 1.508 | 2.229 | 0,035 | 8 / 8 | — | — |
| 49402 | `VCS_VIC13` / `VCS_VIC13` | Dân thường | 0,208 | 0,209 | 1.600 | 2.303 | 0,055 | 8 / 8 | — | — |
| 49403 | `VCS_VIC14` / `VCS_VIC14` | Dân thường | 0,204 | 0,205 | 1.510 | 2.216 | 0,058 | 6 / 6 | — | — |
| 49404 | `VCS_VIC15` / `VCS_VIC15` | Dân thường | 0,208 | 0,209 | 1.686 | 2.421 | 0,047 | 8 / 8 | — | — |
| 49405 | `VCS_VIC2` / `VCS_VIC2` | Dân thường | 0,216 | 0,217 | 1.686 | 2.421 | 0,055 | 8 / 8 | — | — |
| 49406 | `VCS_VIC3` / `VCS_VIC3` | Dân thường | 0,185 | 0,188 | 1.504 | 2.272 | 0,036 | 7 / 7 | — | — |
| 49407 | `VCS_VIC4` / `VCS_VIC4` | Dân thường | 0,211 | 0,213 | 1.634 | 2.314 | 0,056 | 8 / 8 | — | — |
| 49408 | `VCS_VIC5` / `VCS_VIC5` | Dân thường | 0,218 | 0,221 | 1.594 | 2.325 | 0,064 | 7 / 7 | — | — |
| 49409 | `VCS_VIC6` / `VCS_VIC6` | Dân thường | 0,201 | 0,203 | 1.500 | 2.237 | 0,053 | 8 / 8 | — | — |
| 49410 | `VCS_VIC7` / `VCS_VIC7` | Dân thường | 0,230 | 0,232 | 1.646 | 2.365 | 0,073 | 7 / 7 | — | — |
| 49411 | `VCS_VIC8` / `VCS_VIC8` | Dân thường | 0,216 | 0,219 | 1.508 | 2.230 | 0,068 | 6 / 6 | — | — |
| 49412 | `VCS_VIC9` / `VCS_VIC9` | Dân thường | 0,234 | 0,236 | 1.610 | 2.314 | 0,080 | 9 / 9 | — | — |
| 49413 | `VCS_WFOM` / `VCS_WFOM` | Dân thường | 0,243 | 0,246 | 2.072 | 3.072 | 0,043 | 9 / 7 | — | — |
| 49414 | `BW_SCH_ENGLISH2` / `BW_SCH_ENGLISH2` | Dân thường | 0,364 | 0,367 | 1.546 | 1.404 | 0,258 | 3 / 3 | — | — |
| 49415 | `BW_SWAT` / `BW_SWAT` | Cảnh sát / quân đội / cứu hộ | 0,212 | 0,215 | 1.740 | 1.561 | 0,094 | 2 / 4 | — | — |
| 49416 | `BW_ARMY` / `BW_ARMY` | Cảnh sát / quân đội / cứu hộ | 0,295 | 0,297 | 2.623 | 1.936 | 0,141 | 5 / 6 | — | — |
| 49417 | `BW_AS_PATIENT` / `BW_AS_PATIENT` | Dân thường | 0,338 | 0,340 | 1.334 | 1.120 | 0,250 | 2 / 2 | — | — |
| 49418 | `BW_ASSOCIATE` / `BW_ASSOCIATE` | Dân thường | 0,339 | 0,342 | 1.382 | 1.130 | 0,250 | 2 / 2 | — | — |
| 49419 | `BW_BMYBWB4` / `BW_BMYBWB4` | Dân thường | 0,432 | 0,434 | 1.336 | 1.348 | 0,333 | 1 / 1 | — | — |
| 49420 | `BW_BMYBWB5` / `BW_BMYBWB5` | Dân thường | 0,396 | 0,398 | 968 | 761 | 0,333 | 1 / 1 | — | — |
| 49421 | `BW_FBI` / `BW_FBI` | Cảnh sát / quân đội / cứu hộ | 0,269 | 0,271 | 1.810 | 1.411 | 0,156 | 5 / 6 | — | — |
| 49422 | `BW_MEDIC` / `BW_MEDIC` | Cảnh sát / quân đội / cứu hộ | 0,156 | 0,158 | 1.104 | 912 | 0,083 | 1 / 1 | — | — |

Metadata và nguồn archive/offset/hash/texture từng ảnh: [census JSON](evidence/eagle-current-skin-census.json).
