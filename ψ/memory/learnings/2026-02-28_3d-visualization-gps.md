# Lesson Learned: Smooth GPS Path Interpolation in 3D (Three.js)

**Date**: 2026-02-28
**Topic**: Data Visualization / 3D Animation

## Context
ในการสร้าง 3D Travel Map จากข้อมูล GPS (Lat, Lon) ข้อมูลมักจะมาเป็นจุดๆ ที่มีระยะห่างไม่เท่ากัน หากให้รถไฟเคลื่อนที่ตรงๆ ระหว่างจุด (Linear Interpolation) จะทำให้การเคลื่อนที่ดู "กระตุก" และไม่สมจริง

## The Learning
การใช้ `CatmullRomCurve3` ใน Three.js สามารถเปลี่ยนชุดพิกัด Vector3 ให้กลายเป็นเส้นโค้งที่ต่อเนื่องและนุ่มนวลได้:

1. **Projection**: แปลงพิกัด Lat/Lon เป็น 3D Vector3 โดยใช้ค่า Scale ที่เหมาะสม (เช่น 800 units ต่อ 1 องศา)
2. **Curve Generation**: `const curve = new THREE.CatmullRomCurve3(points);`
3. **Animation**: ใช้ฟังก์ชัน `.getPointAt(fraction)` เพื่อดึงตำแหน่งบนเส้นโค้ง ณ เวลาที่กำหนด (0.0 - 1.0)
4. **Orientation**: การใช้ `.lookAt()` ไปยังจุดถัดไป (`fraction + delta`) ช่วยให้ขบวนรถไฟหันหน้าไปตามทิศทางของเส้นทางได้อย่างถูกต้อง

## Concept Tags
- #threejs #datavis #gps #animation #splines #smile-oracle
