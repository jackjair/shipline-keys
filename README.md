# Shipline 安裝程式簽章公鑰

這個 repo 只放 Shipline 安裝程式（`https://shipline.netsurf.tw/install`）的簽章公鑰，放在 Shipline 伺服器以外的地方，讓你比對。
私鑰只在維運者的電腦上，從沒放上伺服器。

- 公鑰（`ssh-keygen -Y` 的 allowed_signers 格式）：[`release-keys`](release-keys)
- 指紋：`SHA256:0flIMAfWRe/BTgMHQqtnzcUytF8R1h7yLrB+NdjUsoI`（ED25519）
- 簽章身分 `shipline-release`、namespace `shipline-install`

## 第一次安裝前自己驗證（選用）

```bash
curl -fsSL https://shipline.netsurf.tw/install -o shipline-install.sh
curl -fsSL https://shipline.netsurf.tw/install.sig -o shipline-install.sh.sig
curl -fsSL https://raw.githubusercontent.com/jackjair/shipline-keys/main/release-keys -o shipline-release-keys
ssh-keygen -Y verify -f shipline-release-keys -I shipline-release -n shipline-install -s shipline-install.sh.sig < shipline-install.sh
```

看到 `Good "shipline-install" signature for shipline-release` 才執行：`SHIPLINE_PAIR_CODE=<網頁上的配對碼> bash shipline-install.sh`。

## 已經裝過的電腦

用 `bash ~/.shipline/install.sh --update`。它會用安裝時存在 `~/.shipline/release-keys` 的公鑰自動驗證網站上的新版，驗不過就停下、什麼都不改。

## 換金鑰紀錄

| 日期 | 指紋 | 說明 |
|---|---|---|
| 2026-10-05 | `SHA256:0flIMAfWRe/BTgMHQqtnzcUytF8R1h7yLrB+NdjUsoI` | 第一把 |

換金鑰時，新公鑰會由舊私鑰簽過的安裝程式帶過去，並記在上表。
