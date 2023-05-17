# 实体在平面坐标系上移动
该方法是绑定在特定对象上的方法，该对象具有长度为 2 的数组 `pos` 属性记录坐标。

## 代码
``` javascript linenums="1"
/**
 * 实体在平面坐标系上移动
 * @param {Number} angle 角度
 * @param {Number} [distance] 移动距离
 * @returns {Array<Number>} 移动后的坐标
 */
function move(angle, distance) {
    if (distance <= 0) return this.pos;
    if (angle >= 360 || angle <= -360) return; 
    let x = this.pos[0];
    let y = this.pos[1];

    switch (angle) {
        case 0:
            x += distance;
            break;
            
        case 90:
        case -270:
            y += distance;
            break;
        
        case 180:
        case -180:
            x -= distance;
            break;

        case 270:
        case -90:
            y -= distance;
            break;
    
        default:
            let dx = Math.cos(angle * Math.PI/180) * distance + x;
            let dy = Math.sin(angle * Math.PI/180) * distance + y;
            return this.pos = [dx, dy];
    }
    
    return this.pos = [x, y];
}
```

## 效果
- 若移动距离小于等于 0，则不移动，返回实体当前坐标。
- 若角度大于 360 或小于 -360，则失败，返回空值。
- 其余情况下，移动成功，返回移动后的坐标。