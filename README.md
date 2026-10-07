# kokoro — giọng đọc tiếng Trung trên máy / on-device Mandarin voice

Bản phát hành `kokoro-zh-v1` chứa gói giọng đọc tiếng Phổ thông (Kokoro v1.1-zh,
int8, chạy offline bằng [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx))
cho ứng dụng **Học Tiếng Trung**. Repo này chỉ để lưu file phát hành; mã nguồn
ứng dụng không ở đây.

Release `kokoro-zh-v1` holds the on-device Mandarin voice package (Kokoro
v1.1-zh, int8, offline via sherpa-onnx) used by the app *Học Tiếng Trung*.
This repository only hosts the release files.

## Nguồn / Sources

- Model: [hexgrad/Kokoro-82M-v1.1-zh](https://huggingface.co/hexgrad/Kokoro-82M-v1.1-zh) — Apache-2.0.
- ONNX int8 export, `tokens.txt`, `lexicon-zh.txt`, `phone/date/number-zh.fst`:
  sherpa-onnx `kokoro-int8-multi-lang-v1_1`
  ([k2-fsa/sherpa-onnx releases `tts-models`](https://github.com/k2-fsa/sherpa-onnx/releases/tag/tts-models)) — Apache-2.0.
- `espeak-ng-data/` (phontab, phonindex, phondata, intonations, en_dict,
  lang/gmw/en-US): [eSpeak NG](https://github.com/espeak-ng/espeak-ng) —
  GPL-3.0-or-later (`LICENSE-espeak-ng`). sherpa-onnx cannot start this model
  without it; it only voices non-Chinese runs (Latin letters, mixed punctuation).

## Giọng giữ lại / Speakers kept

`voices.bin` chỉ giữ 2 trong 103 giọng gốc / keeps 2 of the original 103:

| index | giọng / voice | id gốc / original sid | tên / name |
|---|---|---|---|
| 0 | nữ / female | 34 | `zf_059` |
| 1 | nam / male | 77 | `zm_050` |

`model.int8.onnx`: chỉ sửa metadata số giọng / only the speaker metadata
(`n_speakers`, `speaker_names`, `speaker2id`, `id2speaker`) was rewritten;
weights and graph are byte-identical to the original. See `NOTICE`.

## Tải về và ghép / Download and reassemble

Ứng dụng tự tải và kiểm tra. Làm tay / by hand:

```bash
base=https://github.com/LongKhoa0706/kokoro/releases/download/kokoro-zh-v1/
for p in kokoro-zh-v1.tar.gz.part00 kokoro-zh-v1.tar.gz.part01 kokoro-zh-v1.tar.gz.part02; do curl -LO "$base$p"; done
cat kokoro-zh-v1.tar.gz.part* > kokoro-zh-v1.tar.gz
shasum -a 256 kokoro-zh-v1.tar.gz   # a7d19d87a48f8a8ac3d70a38461c20528ea82b2e04481416abb8b098d4cb8b16
tar xzf kokoro-zh-v1.tar.gz         # -> kokoro-zh-v1/ (manifest.json lists sha256 of every file)
```

Archive `kokoro-zh-v1.tar.gz`: 90,809,168 bytes, sha256 `a7d19d87a48f8a8ac3d70a38461c20528ea82b2e04481416abb8b098d4cb8b16`.
Unpacked: 118,538,542 bytes.

| part | bytes | sha256 |
|---|---|---|
| `kokoro-zh-v1.tar.gz.part00` | 45,000,000 | `50e0a8f54a3d1eeae7a72efb847284a6574cb463292460e4f12d6932cfa38d07` |
| `kokoro-zh-v1.tar.gz.part01` | 45,000,000 | `a5f760d9f92a54417d47c8cc5cbd9f1a53f6acd2ef15d1a426f5c7f45e01de52` |
| `kokoro-zh-v1.tar.gz.part02` | 809,168 | `9bcbb4d3588bdb012d7061a1e6e53573e5ef6e2c16fa8df7c9d90df85186307d` |

`kokoro-zh-v1.release.json` mô tả các phần trên (máy đọc) / machine-readable list of the parts.

## Nội dung gói / Package content (`kokoro-zh-v1/`)

| file | bytes |
|---|---|
| `LICENSE` | 11,358 |
| `LICENSE-espeak-ng` | 35,147 |
| `NOTICE` | 1,265 |
| `date-zh.fst` | 59,154 |
| `espeak-ng-data/en_dict` | 166,944 |
| `espeak-ng-data/intonations` | 2,040 |
| `espeak-ng-data/lang/gmw/en-US` | 257 |
| `espeak-ng-data/phondata` | 550,424 |
| `espeak-ng-data/phonindex` | 39,074 |
| `espeak-ng-data/phontab` | 55,796 |
| `lexicon-zh.txt` | 2,119,465 |
| `model.int8.onnx` | 114,296,074 |
| `number-zh.fst` | 64,482 |
| `phone-zh.fst` | 88,630 |
| `tokens.txt` | 1,111 |
| `voices.bin` | 1,044,480 |
| `manifest.json` | — |

## Giấy phép / License

Apache-2.0 (`LICENSE`) cho mô hình, lexicon, FST / for the model, lexicon and
FSTs; GPL-3.0-or-later (`LICENSE-espeak-ng`) cho / for `espeak-ng-data/`.
Ghi công và thay đổi / attribution and changes: `NOTICE`.
