# 保持尺寸大小压缩图片
```
    /**
     * 保持尺寸大小压缩图片
     *
     * @param pBitmap  图片信息
     * @param pFormat  图片格式
     * @param pMaxSize 压缩后的最大字节长度（单位：KB）
     * @return 
     */
    public static byte[] getCompressWebpBitMap(Bitmap pBitmap, Bitmap.CompressFormat pFormat, int pMaxSize) {
        boolean goon = true;
        int options = 100;

        ByteArrayOutputStream lOutputStream = new ByteArrayOutputStream();
        pBitmap.compress(pFormat, options, lOutputStream);
        Log.i("getCompressWebpBitMap", "original size:" + (lOutputStream.toByteArray().length / 1024) + "KB");

        try {
            while (goon) {
                lOutputStream.reset();
                pBitmap.compress(Bitmap.CompressFormat.WEBP, options, lOutputStream);
                if (lOutputStream.toByteArray().length / 1024 > pMaxSize) {
                    options -= 5;
                } else {
                    goon = false;
                }
            }
        } catch (Exception pE) {
            Log.i("getCompressWebpBitMap", "error:" + pE.getMessage());
        }
        Log.i("getCompressWebpBitMap", "final size:" + (lOutputStream.toByteArray().length / 1024) + "KB");
        return lOutputStream.toByteArray();
    }
```
