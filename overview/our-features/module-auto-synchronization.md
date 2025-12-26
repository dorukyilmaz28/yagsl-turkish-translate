# Modül Otomatik Senkronizasyonu

YAGSL, dahili enkoder ile mutlak enkoder arasındaki fark (delta) ölü bandı (deadband) aştığında ve modül yarım saniye boyunca hareketsiz kaldığında, açı/dümenleme/azimut motor kontrolcülerinin mutlak enkoderlerini ve dahili enkoderlerini otomatik olarak senkronize eder.

Bu, ilk parametrenin etkin durumu ve ikincisinin derece cinsinden ölü bant olduğu `SwerveDrive.setModuleEncoderAutoSynchronize(bool, double)` aracılığıyla yapılandırılabilir.
