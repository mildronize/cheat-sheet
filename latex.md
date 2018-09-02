# Latex

### ใช้ภาษาไทย

* ใช้ `xelatex` แทน `latex` นะ

### Editer

ตั้งแต่ลองมาหลายตัว `TexStudio` work สุดแล้ว

### การ debug latex

1. Error Message ไม่ได้บอกอะไรได้มาก  ดังนั้น
   * เซฟบ่อยๆ ยึดโค๊ดที่คอมไพล์ผ่านเป็นหลัก
   * ใช้ git ช่วยจะดีมาก เอาไว้ย้อนเวอร์ชั่นกลับ

### References

#### URL Ref

1. use `@misc`
2. use `howpublished` instead of `url`
3. ใช้ latex package `url` ในการทำ word wrap
4. ระวังอักขระพิเศษ เช่น `#` ให้ใช้ `\#` แทน

```text
@misc{prometheus_vs_opentsdb,
    title = {COMPARISON TO ALTERNATIVES, Prometheus vs. OpenTSDB},
    howpublished = {\url{https://prometheus.io/docs/introduction/comparison/\#prometheus-vs.-opentsdb}},
    urldate = {2016-07-10},
    month = jul,
    year = {2016},
}
```

```diff

```

