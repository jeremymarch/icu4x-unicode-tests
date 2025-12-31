# Tests for Rust's ICU4X Collator

Install icu4x-datagen with (version should match version of library):  
cargo install icu4x-datagen --version 2.1.1 --force

Generate the minimal Greek collation data, run:  
icu4x-datagen --format blob --locales el --markers all --out greek_collation_blob.postcard  

Start with the above which includes all el data.  Then compile with this:  

cargo build --release && icu4x-datagen --markers-for-bin target/release/librust_icu4x_test.rlib --locales el --format blob --out greek_collation_blob.postcard --overwrite

The --markers-for-bin option includes only the keys used in the binary.  So this may need to be run three times: first to create the binary, then to generate the data based on the binary, and a third time to embed this generated data inside the binary.

For the locale, just used "el" for icu4x-datagen. In the code, you can specify preferences such as "el-u-kn-true", which is used to sort numbers numerically rather than as strings.

Reference:  
https://www.credativ.de/en/blog/credativ-inside/icu4x-what-it-can-do-and-how-to-do-it/  
https://github.com/unicode-org/icu4x/blob/main/tutorials/data-management.md
