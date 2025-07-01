<！doctype html>
<超文本标记语言朗="en">
<头>
<元字符集="UTF-8">
<元姓名="视口" 内容="宽度=设备宽度，初始比例=1.0">
<标题>樱花爱心</标题>
<风格>
身体{
边缘: 0;
溢出: 隐藏的;
背景: #000;
        }
帆布{
显示: 块;
        }
</风格>
</头>
<身体>
<帆布身份标识="画布"></帆布>
<脚本>
Const帆布=文档.getElementById('画布')；
Const CTX=画布。getContext('2d')；
帆布。宽度=窗口。innerWidth；
帆布。 高度=窗口。 内高度；

    // 樱花参数
    Const PETAL_COUNT=500；//花瓣数量（可调整密集度）
    常数花瓣=[]；
    Const petalColors=['#FFB6C1'，'#FFC0CB'，'#FF69B4'，'#DB7093'，'#FFA07A']；
    Const heartParticle=[]；
    常数名称="杨彩云"；//名字

    // 樱花类（真实飘落效果）
    樱花花瓣{
    构造函数(){
    this.reset()；
    this.size=Math.random()*8+3；
    this.rotation=Math.random()*Math.PI*2；
    this.rotationSpeed=Math.random()*0.1-0.05；
    this.wind=Math.random()*0.5-0.25；
    这。 颜色=花瓣颜色[数学地板(数学随机()*花瓣颜色。 长度)]；
    this.opacity=Math.random()*0.5+0.3；
    // 五瓣樱花形状控制点
    this.points=[]；
    for(设i=0；i<5；i++){
    常数角度=(i*72+Math.random()*20-10)*Math.PI/180；
    常数半径=this.size*(0.8+Math.random()*0.4)；
    this.points.push({
    X:Math.cos(角度)*半径，
    y:Math.sin(角度)*半径
                    });
                }
            }
    重置(){
    this.x=Math.random()*canvas.width；
    this.y=Math.random()*-200-50；
    this.speed=Math.random()*2+1；
    this.angle=Math.random()*Math.PI*2；
            }
    画(){
    ctx.save()；
    ctx.translate(this.x，this.y)；
    ctx.rotate(this.rotation)；
    ctx.globalAlpha=this.opacity；
    ctx.fillStyle=this.color；
    ctx.beginPath()；
    // 绘制五瓣樱花（贝塞尔曲线模拟真实花瓣）
    ctx.moveTo(0，0)；
    for(设i=0；i<5；i++){
    const p1=this.points[i]；
    const p2=this.points[(i+1)%5]；
    const midx=(p1.x+p2.x)*0.5；
    Const Midy=(p1.y+p2.y)*0.5；
    ctx.quadraticCurveTo(p1.x，p1.y，midx，Midy)；
                }
    ctx.closePath()；
    ctx.fill()；
    ctx.restore()；
            }
    更新(){
    this.y+=this.speed；
    this.x+=Math.sin(this.angle)*0.8+this.wind；
    this.rotation+=this.rotationSpeed；
    此角度+=0.01；
    // 花瓣重置
    if(this.y>画布。高度+50||this.x<-50||this.x>画布。宽度+50){
    this.reset()；
                }
    this.draw()；
            }
        }

    // 爱心粒子
    类HeartParticle{
    构造函数(x，y){
    this.baseX=x；
    this.baseY=y；
    this.x=x；
    this.y=y；
    this.size=Math.random()*3+2；
    this.density=Math.random()*10+5；
            }
    画(){
    // 樱花替代简单粒子
    ctx.save()；
    ctx.translate(this.x，this.y)；
    ctx.rotate(Date.now()*0.001)；
    CTX.fillStyle=花瓣颜色[数学下限(数学随机()*花瓣颜色。长度)]；
    ctx.globalAlpha=0.7；
    ctx.beginPath()；
    // 简化版五瓣樱花
    for(设i=0；i<5；i++)
    Const Angle=i*72*Math.PI/180；
    恒定半径=此尺寸；
    ctx.lineTo(Math.cos(角度)*半径，Math.sin(角度)*半径)；
                }
    ctx.closePath()；
    ctx.fill()；
    ctx.restore()；
            }
    更新()
    // 心跳效果
    Const dx=Math.sin(Date.now()*0.001)*3；
    Const dy=Math.cos(Date.now()*0.002)*5；
this.x=this.baseX+dx；
this.y=this.baseY+dy；
this.draw()；
            }
        }

    // 爱心形状
    函数initHeart(){
    for(设t=0；t<2*Math.PI；t+=0.03){
    Const x=16*Math.pow(Math.sin(t)，3)；
    Const y=-(13*Math.Cos(t)-5*Math.Cos(2*t)-2*数学Cos(3*t)-数学Cos(4*t))；
    Const scale=12；
    heartParticle.push(新HeartParticle(
    canvas.width/2+x*scale，
    画布.高度/2+y*比例
                ));
            }
        }

    // 初始化飘落樱花
    函数initPetals(){
    for(让i=0；i<PETAL_COUNT；i++){
    花瓣。 推(新樱花花瓣())；
            }
        }

    // 动画循环
    函数使有生气(){
    CTX.clearRect(0，0，画布。宽度，画布。高度)；
            
    // 樱花爱心
    for(让heartParticles的粒子){
    particle.update()；
            }
            
    // 绘制名字
    ctx.font='bold30px Arial'；
    ctx.shadowColor='#FF69B4'；
    ctx.shadowBlur=15；
    ctx.fillStyle='白色'；
    ctx.textAlign='center'；
    CTX.fillText(名称，画布。宽度/2，画布。高度/2)；
    ctx.shadowBlur=0；
            
    // 更新飘落樱花
    for(让花瓣中的花瓣){
    petal.update()；
            }
            
    requestAnimationFrame(animate)；
        }

    // 启动
    initHeart()；
    initPetals()；
    使有生气()；

    // 窗口大小调整
    window.addEventListener('resize'，()=>{
    canvas.width=window.innerWidth；
    canvas.height=window.innerHeight；
    heartParticle.length=0；
    initHeart()；
        });
    </script>
</身体>
</超文本标记语言>
