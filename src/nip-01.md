# نیپ شماره ۱

## روشنگری بنیادی روند پروتکل

`پیشنویس` ‍‍‍‍`بایسته(الزامی)`

این نیپ  پروتکل آغازینی را میشناساند که باید توسط همه پیاده سازی شود. نیپ های تازه تر ممکن است زمینه ها پیام ها و یا قابلیت های دلخواهی به روند شناسانده شده (معرفی شده) در این نیپ بیفزایند.

## رویداد ها و امضا ها
هر کاربر یک جفت کلید دارد. امضا ها کلید های عمومی و رمزگذاری ها بر اساس استاندارد [Schnorr signatures standard for the curve `secp256k1`](https://bips.xyz/340) انجام میشود.

تنها شی (حالت داده) موجود ‍‍`رویداد` است که فرمت زیر را دارد:

```jsonc
{
  "id": <32-bytes lowercase hex-encoded sha256 of the serialized event data>, // شناسه
  "pubkey": <32-bytes lowercase hex-encoded public key of the event creator>, // کلید عمومی
  "created_at": <unix timestamp in seconds>, // زمان ساخت شدن رویداد
  "kind": <integer between 0 and 65535>, // نوع

  "tags": [ // برچسب ها
    [<arbitrary string>...],
    // ...
  ],
  "content": <arbitrary string>, // محتوا
  "sig": <64-bytes lowercase hex of the signature of the sha256 hash of the serialized event data, which is the same as the "id" field> // امضا
}
```

برای محاسبه شناسه رویداد هش sha256 حالت سریالایز شده ان را محاسبه میکنیم. 