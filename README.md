# gpiomem_rk3568

To compile the driver, the source code need to be integrated to the kernel source into the folder:

```
drivers/char
```
Next, this patches need to be implemented:
```
diff --git a/drivers/char/Makefile b/drivers/char/Makefile
index b8d42b4e979b..abe37487e15f 100644
--- a/drivers/char/Makefile
+++ b/drivers/char/Makefile
@@ -58,3 +58,4 @@ js-rtc-y = rtc.o
 obj-$(CONFIG_XILLYBUS)         += xillybus/
 obj-$(CONFIG_POWERNV_OP_PANEL) += powernv-op-panel.o
 obj-$(CONFIG_ADI)              += adi.o
+obj-$(CONFIG_ARCH_ROCKCHIP)    += rk3568-gpiomem.o

diff --git a/arch/arm64/boot/dts/rockchip/rk3568-odroid.dtsi b/arch/arm64/boot/dts/rockchip/rk3568-odroid.dtsi
index a7a50f0d0762..5cff3df8faa7 100644
--- a/arch/arm64/boot/dts/rockchip/rk3568-odroid.dtsi
+++ b/arch/arm64/boot/dts/rockchip/rk3568-odroid.dtsi
@@ -223,6 +224,14 @@
        test-power {
                status = "okay";
        };
+
+ 
+       rk3568-gpiomem {
+               compatible = "rockchip,rk3568-gpiomem";
+               reg = <0x0 0xfd660000 0x0 0x1000>;
+               status = "okay";
+       };
+
 };
 
 &bus_npu {

```

