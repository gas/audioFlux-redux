# Documentación del Directorio Local

---

## Estructura del Directorio
```
./
├── directorio_local_documentado.md
├── LICENSE.md
├── README.md
└── src/
    ├── bft_algorithm.c
    ├── bft_algorithm.h
    ├── CMakeLists.txt
    ├── cqt_algorithm.c
    ├── cqt_algorithm.h
    ├── dsp/
    │   ├── fft_algorithm.c
    │   ├── fft_algorithm.h
    │   ├── flux_correct.c
    │   ├── flux_correct.h
    │   ├── flux_window.c
    │   ├── flux_window.h
    │   ├── phase_vocoder.c
    │   └── phase_vocoder.h
    ├── filterbank/
    │   ├── auditory_filterBank.c
    │   ├── auditory_filterBank.h
    │   ├── cqt_filterBank.c
    │   └── cqt_filterBank.h
    ├── flux_base.h
    ├── flux_spectral.c
    ├── flux_spectral.h
    ├── flux_temporal.c
    ├── flux_temporal.h
    ├── mir/
    │   ├── onset_algorithm.c
    │   ├── onset_algorithm.h
    │   ├── _queue.c
    │   └── _queue.h
    ├── reassign_algorithm.c
    ├── reassign_algorithm.h
    ├── stft_algorithm.c
    ├── stft_algorithm.h
    ├── temporal_algorithm.c
    ├── temporal_algorithm.h
    ├── util/
    │   ├── flux_util.c
    │   ├── flux_util.h
    │   ├── flux_wave.c
    │   └── flux_wave.h
    └── vector/
        ├── flux_complex.c
        ├── flux_complex.h
        ├── flux_vector.c
        ├── flux_vector.h
        ├── flux_vectorInt.c
        ├── flux_vectorOp.c
        └── flux_vectorOp.h
```

---

## Contenido de los Archivos

### Archivo: `./src/vector/flux_complex.h`

```


#ifndef FLUX_COMPLEX_H
#define FLUX_COMPLEX_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>


// 复数基本运算
void __complexMul(float real1,float image1,
				float real2,float image2,
				float *real3,float *image3);
void __complexDiv(float real1,float image1,
				float real2,float image2,
				float *real3,float *image3);

float __complexMulM(float real1,float image1,
				float real2,float image2);
float __complexDivM(float real1,float image1,
				float real2,float image2);
float __complexPowM(float real,float image,int n);

// n1*m1@m1*n2
void __mcdot(float *mRealArr1,float *mImageArr1,
			float *mRealArr2,float *mImageArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			float *mRealArr3,float *mImageArr3);

// n1*m1@n2*m1
void __mcdot1(float *mRealArr1,float *mImageArr1,
			float *mRealArr2,float *mImageArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			float *mRealArr3,float *mImageArr3);

int __mcdot2(float *mRealArr1,float *mImageArr1,
			float *mRealArr2,float *mImageArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			int *type,
			float *mRealArr3,float *mImageArr3);

// 复数矩阵div
void __mcdiv(float *mRealArr1,float *mImageArr1,
			float *mRealArr2,float *mImageArr2,
			int nLength,int mLength,
			float *mRealArr3,float *mImageArr3);

void __mccut(float *mRealArr1,float *mImageArr1,
			int nLength,int mLength,
			int nIndex,int nLength1,
			int mIndex,int mLength1,
			float *mRealArr3,float *mImageArr3);

// new/convert
void __vcnew(int length,float *value,float **realArr,float **imageArr);
void __vcz2p(float *realArr,float *imageArr,int length,float *rArr,float *tArr);
void __vcp2z(float *rArr,float *tArr,int length,float *realArr,float *imageArr);

// arg/abs/conj   
void __vcarg(float *realArr1,float *imageArr1,int length,float *vArr1);
void __vcangle(float *realArr1,float *imageArr1,int length,float *vArr1);
void __vcabs(float *realArr1,float *imageArr1,int length,float *vArr1);
void __vcsquare(float *realArr1,float *imageArr1,int length,float *vArr1);
void __vcconj(float *realArr1,float *imageArr1,int length,float *realArr3,float *imageArr3);

void __mcabs(float *mRealArr,float *mImageArr,int nLength,int mLength,int axis,float *mArr2);
void __mcabs1(float *mRealArr,float *mImageArr,int nLength,int mLength,int axis,int cutLength,float *mArr2);
void __mcabs2(float *mRealArr,float *mImageArr,int nLength,int mLength,int mLength2,float *mArr2);

void __mcsquare(float *mRealArr,float *mImageArr,int nLength,int mLength,int axis,float *mArr2);
void __mcsquare1(float *mRealArr,float *mImageArr,int nLength,int mLength,int axis,int cutLength,float *mArr2);
void __mcsquare2(float *mRealArr,float *mImageArr,int nLength,int mLength,int mLength2,float *mArr2);

// add/sub/mul/div
void __vcmul(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *realArr3,float *imageArr3);
void __vcdiv(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *realArr3,float *imageArr3);
void __vcadd(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *realArr3,float *imageArr3);
void __vcsub(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *realArr3,float *imageArr3);

void __vcmul_value(float *realArr1,float *imageArr1,
				float rValue,float iValue,int length,
				float *realArr3,float *imageArr3);
void __vcdiv_value(float *realArr1,float *imageArr1,
				float rValue,float iValue,int length,
				float *realArr3,float *imageArr3);
void __vcadd_value(float *realArr1,float *imageArr1,
				float rValue,float iValue,int length,
				float *realArr3,float *imageArr3);
void __vcsub_value(float *realArr1,float *imageArr1,
				float rValue,float iValue,int length,
				float *realArr3,float *imageArr3);

// mul/div 快速求模算法
void __vcmulm(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *vArr3);
void __vcdivm(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *vArr3);
void __vcmulm_value(float *realArr1,float *imageArr1,
				float rValue,float iValue,int length,
				float *realArr3,float *imageArr3);
void __vcdivm_value(float *realArr1,float *imageArr1,
				float rValue,float iValue,int length,
				float *realArr3,float *imageArr3);

// power
void __vcpower1(float r,float t,float *vArr,int length,float *realArr1,float *imageArr1);


// polyval 多项式 阶数有小到大排列
void __vcpolyval(float *wArr1,int length1,float *vArr2,int length2,float *realArr3,float *imageArr3);

// debug相关
void __vcdebug(float *realArr1,float *imageArr1,int length,int type);
void __mcdebug(float *realArr1,float *imageArr1,int nLength,int mLength,int type);


#ifdef __cplusplus
}
#endif





#endif




```

---

### Archivo: `./src/vector/flux_vectorInt.c`

```
// 

#include <string.h>
#include <math.h>

#include "flux_vector.h"

int *__vnewi(int length,int *value){
	int *arr=NULL;
	int _value=0;

	arr=(int *)calloc(length, sizeof(int ));
	if(value){
		_value=*value;
	}

	if(_value!=0){
		for(int i=0;i<length;i++){
			arr[i]=_value;
		}
	}
	
	return arr;
}

int __varangei(int start,int stop,int step,int **outArr){
	int *arr=NULL;
	int length=0;

	if(stop<=start||!outArr){
		return 0;
	}

	length=ceilf((stop-start)/step);
	arr=__vnewi(length, NULL);
	for(int i=0;i<length;i++){
		arr[i]=start+i*step;
	}

	*outArr=arr;
	return length;
}

void __vfilli(int *arr,int length,int value){

	for(int i=0;i<length;i++){
		arr[i]=value;
	}
}

void __vcopyi(int *dstArr,int *srcArr,int length){

	memcpy(dstArr, srcArr, sizeof(float )*length);
}

void __vdebugi(int *vArr1,int length,int type){
	if(type){
		printf("vector is:\n");

		printf("	");
		for(int i=0;i<length;i++){
			printf("%d:%d ,",i,vArr1[i]);
		}
	}
	else{
		printf("vector([");
		for(int i=0;i<length-1;i++){
			printf("%d, ",vArr1[i]);
		}
		printf("%d",vArr1[length-1]);
		printf("])\n");
	}
}

void __mdebugi(int *mArr1,int nLength,int mLength,int type){
	if(type){
		printf("matrix is:\n");

		for(int i=0;i<nLength;i++){
			printf("	%d:\n",i);
			printf("		");
			for(int j=0;j<mLength;j++){
				printf("%d:%d ,",j,mArr1[i*mLength+j]);
			}

			printf("\n\n");
		}
	}
	else{
		printf("matrix([");
		for(int i=0;i<nLength-1;i++){
			printf("[");

			for(int j=0;j<mLength-1;j++){
				printf("%d ,",mArr1[i*mLength+j]);
			}
			printf("%d",mArr1[i*mLength+mLength-1]);

			printf("],");
			printf("\n        ");
		}

		printf("[");
		for(int j=0;j<mLength-1;j++){
			printf("%d ,",mArr1[(nLength-1)*mLength+j]);
		}
		printf("%d",mArr1[(nLength-1)*mLength+mLength-1]);

		printf("]");
		printf("])\n");
	}
}

void __vsubi(int *vArr1,int *vArr2,int length,int *vArr3){
	int *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]-vArr2[i];
	}
}



```

---

### Archivo: `./src/vector/flux_vector.h`

```


#ifndef FLUX_VECTOR_H
#define FLUX_VECTOR_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

typedef struct{
	int nLength;
	int mLength;

	int *indexArr; // _v使用nLength _m nLength+mLength

} VSlice;

// univers function op
typedef float (*UniFunc)(float element);
typedef float (*UniFunc1)(float element,float value);

// dot/mul/div/add/sub sum/min/max/mean
// n1*m1@m1*n2
void __mdot(float *mArr1,float *mArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			float *mArr3);

// n1*m1@n2*m1
void __mdot1(float *mArr1,float *mArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			float *mArr3);

int __mdot2(float *mArr1,float *mArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			int *type,
			float *mArr3);

void __msub(float *mArr1,float *mArr2,int nLength,int mLength,float *mArr3);

/***
	A n*m
	1*m/n*1=>0/1/ => axis 0/1 type 0/1 vArr axis
	注:一般add/sub 同轴 mul/div 非同轴
****/
void __mmul_vector(float *mArr1,float *vArr,int type,int nLength,int mLength,int axis,float *mArr3);
void __mdiv_vector(float *mArr1,float *vArr,int type,int nLength,int mLength,int axis,float *mArr3);
void __madd_vector(float *mArr1,float *vArr,int type,int nLength,int mLength,int axis,float *mArr3);
void __msub_vector(float *mArr1,float *vArr,int type,int nLength,int mLength,int axis,float *mArr3);

void __mmul_value(float *mArr1,float value,int nLength,int mLength,float *mArr3);

// 向量归一化 type 0 p 1/2/3... 1 Inf 2 -Inf
void __mnormalize(float *mArr1,int nLength,int mLength,int axis,int type,float p,float *mArr3);
void __mnorm(float *mArr1,int nLength,int mLength,int axis,int type,float p,float *vArr2);

// order 1
void __mdiff(float *mArr1,int nLength,int mLength,int axis,int *order,float *mArr3);
// step 1
void __mdiff2(float *mArr1,int nLength,int mLength,int axis,int *step,float *mArr3);

void __mmaxfilter(float *mArr1,int nLength,int mLength,int axis,int order,float *mArr3);
void __mmedianfilter(float *mArr1,int nLength,int mLength,int axis,int order,float *mArr3);

/***
	axis 0 row 1 col -1/other all
****/
void __msum(float *mArr1,int nLength,int mLength,int axis,float *vArr3);
void __mmin(float *mArr1,int nLength,int mLength,int axis,float *vArr3,int *indexArr3);
void __mmax(float *mArr1,int nLength,int mLength,int axis,float *vArr3,int *indexArr3);
void __mmean(float *mArr1,int nLength,int mLength,int axis,float *vArr3);

void __mmedian(float *mArr1,int nLength,int mLength,int axis,float *vArr3);
void __mvar(float *mArr1,int nLength,int mLength,int axis,int type,float *vArr3);
void __mstd(float *mArr1,int nLength,int mLength,int axis,int type,float *vArr3);
void __mcov(float *mArr1,float *mArr2,int nLength,int mLength,int axis,int type,float *vArr3);
void __mcorrcoef(float *mArr1,float *mArr2,int nLength,int mLength,int axis,float *vArr3);

void __mrms(float *mArr1,int nLength,int mLength,int axis,float *vArr3);
void __menergy(float *mArr1,int nLength,int mLength,int axis,float *vArr3);
void __mzcr(float *mArr1,int nLength,int mLength,int axis,float *vArr3);

void __munwrap(float *mArr1,int nLength,int mLength,int axis);

float __vdot(float *vArr1,float *vArr2,int length);

void __vmul(float *vArr1,float *vArr2,int length,float *vArr3);
void __vdiv(float *vArr1,float *vArr2,int length,float *vArr3);
void __vadd(float *vArr1,float *vArr2,int length,float *vArr3);
void __vsub(float *vArr1,float *vArr2,int length,float *vArr3);
void __vsubi(int *vArr1,int *vArr2,int length,int *vArr3);

// order 1
void __vdiff(float *vArr1,int length,int *order,float *vArr3);
// step 1
void __vdiff2(float *vArr1,int length,int *step,float *vArr3);

void __vmaxfilter(float *vArr1,int length,int order,float *vArr3);
void __vmedianfilter(float *vArr1,int length,int order,float *vArr3);

void __vmul_value(float *vArr1,float value,int length,float *vArr3);
void __vdiv_value(float *vArr1,float value,int length,float *vArr3);
void __vadd_value(float *vArr1,float value,int length,float *vArr3);
void __vsub_value(float *vArr1,float value,int length,float *vArr3);

// 模/2范式
float __vnorm(float *vArr1,int length);
// 向量归一化 type 0 p 1/2/3... 1 Inf 2 -Inf
void __vnormalize(float *vArr1,int length,int type,float p,float *vArr2);

// 各种scale
void __vminmaxscale(float *vArr1,int length,float *vArr2);
void __vstandscale(float *vArr1,int length,int type,float *vArr2);
void __vmaxabsscale(float *vArr1,int length,float *vArr2);
void __vrobustscale(float *vArr1,int length,float *vArr2);

void __vcenterscale(float *vArr1,int length,float *vArr2);
void __vmeanscale(float *vArr1,int length,float *vArr2);
void __varctanscale(float *vArr1,int length,float *vArr2);

float __vsum(float *vArr1,int length);
int __vsumi(int *vArr1,int length);
int __vmin(float *vArr1,int length,float *value);
int __vmax(float *vArr1,int length,float *value);
int __vmini(int *vArr1,int length,int *value);
int __vmaxi(int *vArr1,int length,int *value);
int __vminabs(float *vArr1,int length,float *value);
int __vmaxabs(float *vArr1,int length,float *value);

float __vmean(float *vArr1,int length);
float __vmedian(float *vArr1,int length);
// 0 默认 N-1 1 N
float __vvar(float *vArr1,int length,int type);
float __vstd(float *vArr1,int length,int type);
float __vcov(float *vArr1,float *vArr2,int length,int type);
float __vcorrcoef(float *vArr1,float *vArr2,int length);

float __vrms(float *vArr1,int length);
float __venergy(float *vArr1,int length);
float __vzcr(float *vArr1,int length);

void __vunwrap(float *vArr1,int length,float *vArr2);

// type 0 asc 1 desc
void __vsort(float *vArr1,int length,int type,float *vArr2);
void __vsorti(int *vArr1,int length,int type,int *vArr2);

void __vcorrsort(float *vArr1,float *vArr2,float *vArr3,int length,int type);
void __vcorrsort1(float *vArr1,float *vArr2,float *vArr3,int *vArr4,int length,int type);

int __vindex(float *vArr1,int length,float value);
int __vindexi(int *vArr1,int length,int value);

int __vhas(float *vArr1,int length,float value);
int __vhasi(int *vArr1,int length,int value);

// univers function op
void __vmap(float *vArr1,int length,void *callback,float *vArr2);
void __vmap1(float *vArr1,int length,void *callback1,float value,float *vArr2);

// new/arange/linspace transpose/index相关
float *__vnew(int length,float *value);
int *__vnewi(int length,int *value);

float *__vlinspace(float start,float stop,int length,int type);
float *__vlogspace(float start,float stop,int length,int type);
int __varange(float start,float stop,float step,float **outArr);
int __varangei(int start,int stop,int step,int **outArr);

void __vfill(float *arr,int length,float value);
void __vfilli(int *arr,int length,int value);

void __vcopy(float *dstArr,float *srcArr,int length);
void __vcopyi(int *dstArr,int *srcArr,int length);

void __mtrans(float *mArr1,int nLength,int mLength,float *mArr3);

float *__vget(float *vArr1,int length,VSlice *slice);
void __vset(float *vArr1,int length,VSlice *slice,float *vArr2);

float *__mget(float *mArr1,int nLength,int mLength,VSlice *slice);
void __mset(float *mArr1,int nLength,int mLength,VSlice *slice,float *mArr2);
void __mset_value(float *mArr1,int nLength,int mLength,VSlice *slice,float value);
void __mset_vector(float *mArr1,int nLength,int mLength,VSlice *slice,int axis,float *vArr1);

// astype
void __vf2i(float *vArr1,int length,int *vArr2);
void __vi2f(int *vArr1,int length,float *vArr2);

// repeat/concat
void __vrepeat(float *vArr1,int length,int num,float *mArr3);
void __mrepeat(float *mArr1,int nLength,int mLength,int axis,int num,float *mArr3);

void __vconcat(float *vArr1,float *vArr2,int length1,int length2,float *vArr3);
void __mconcat(float *mArr1,float *mArr2,
				int nLength1,int mLength1,
				int nLength2,int mLength2,
				int axis,
				float *mArr3);

// 矩阵nLength*mLength内的裁切
void __mcut(float *mArr1,int nLength,int mLength,
			int nIndex,int nLength1,
			int mIndex,int mLength1,
			float *mArr3);

// debug vector/matrix相关 type 0 标准 1 非标准
void __vdebug(float *vArr1,int length,int type);
void __mdebug(float *mArr1,int nLength,int mLength,int type);

void __vdebugi(int *vArr1,int length,int type);
void __mdebugi(int *mArr1,int nLength,int mLength,int type);


#ifdef __cplusplus
}
#endif





#endif




```

---

### Archivo: `./src/vector/flux_complex.c`

```
// 

#include <string.h>
#include <math.h>

#include "flux_complex.h"

#ifdef HAVE_OMP
#include <omp.h>
#endif

extern int __kernelNum;

// 针对 type 0即符合乘法
void __mcdot(float *mRealArr1,float *mImageArr1,
			float *mRealArr2,float *mImageArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			float *mRealArr3,float *mImageArr3){
	if(mLength1!=nLength2){
		return;
	}

	for(int i=0;i<nLength1;i++){
		for(int j=0;j<mLength2;j++){
			double _value1=0;
			double _value2=0;

			float r1=0;
			float r2=0;

			float i1=0;
			float i2=0;

			for(int k=0;k<mLength1;k++){ // arr1.row*arr2.col
				r1=mRealArr1[i*mLength1+k];
				r2=mRealArr2[j+k*mLength2];

				i1=mImageArr1[i*mLength1+k];
				i2=mImageArr2[j+k*mLength2];

				_value1+=(r1*r2-i1*i2);
				_value2+=(i1*r2+r1*i2);
			}

			mRealArr3[i*mLength2+j]=_value1;
			mImageArr3[i*mLength2+j]=_value2;
		}
	}
}

// 针对 type 1即m2转置符合乘法
void __mcdot1(float *mRealArr1,float *mImageArr1,
			float *mRealArr2,float *mImageArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			float *mRealArr3,float *mImageArr3){
	if(mLength1!=mLength2){
		return;
	}

	for(int i=0;i<nLength1;i++){
		for(int j=0;j<nLength2;j++){
			double _value1=0;
			double _value2=0;

			float r1=0;
			float r2=0;

			float i1=0;
			float i2=0;

			for(int k=0;k<mLength1;k++){ // arr1.row*arr2.row
				r1=mRealArr1[i*mLength1+k];
				r2=mRealArr2[j*mLength2+k];

				i1=mImageArr1[i*mLength1+k];
				i2=mImageArr2[j*mLength2+k];

				_value1+=(r1*r2-i1*i2);
				_value2+=(i1*r2+r1*i2);
			}

			mRealArr3[i*nLength2+j]=_value1;
			mImageArr3[i*nLength2+j]=_value2;
		}
	}
}

/***
	n1*m1 n2*m2 => n3*m3
	type
		0 n1*m2 m1==n2
		1 n1*n2 m1==m2
		2 m1*m2 n1==n2
		3 m1*n2 n1==m2
	不能in place操作
	return 0 sucess 1 error
****/
int __mcdot2(float *mRealArr1,float *mImageArr1,
			float *mRealArr2,float *mImageArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			int *type,
			float *mRealArr3,float *mImageArr3){
	int status=0;

	int nLen3=0;
	int mLen3=0;

	int _type=0;

	if(type){
		_type=*type;
	}

	if(_type==0){ // n1*m2
		nLen3=nLength1;
		mLen3=mLength2;
		if(mLength1!=nLength2){
			return -1;
		}
	}
	else if(_type==1){ // n1*n2
		nLen3=nLength1;
		mLen3=nLength2;
		if(mLength1!=mLength2){
			return -1;
		}
	}
	else if(_type==2){ // m1*m2
		nLen3=mLength1;
		mLen3=mLength2;
		if(nLength1!=nLength2){
			return -1;
		}
	}
	else{ // m1*n2
		nLen3=mLength1;
		mLen3=nLength2;
		if(nLength1!=mLength2){
			return -1;
		}
	}

	for(int i=0;i<nLen3;i++){
		for(int j=0;j<mLen3;j++){
			double _value1=0;
			double _value2=0;

			float r1=0;
			float r2=0;

			float i1=0;
			float i2=0;

			if(_type==0){ // n1*m2
				for(int k=0;k<mLength1;k++){ // arr1.row*arr2.col
					r1=mRealArr1[i*mLength1+k];
					r2=mRealArr2[j+k*mLength2];

					i1=mImageArr1[i*mLength1+k];
					i2=mImageArr2[j+k*mLength2];

					_value1+=(r1*r2-i1*i2);
					_value2+=(i1*r2+r1*i2);
				}
			}
			else if(_type==1){ // n1*n2 
				for(int k=0;k<mLength1;k++){ // arr1.row*arr2.T.col(arr2.row)
					r1=mRealArr1[i*mLength1+k];
					r2=mRealArr2[j*mLength2+k];

					i1=mImageArr1[i*mLength1+k];
					i2=mImageArr2[j*mLength2+k];

					_value1+=(r1*r2-i1*i2);
					_value2+=(i1*r2+r1*i2);
				}
			}
			else if(_type==2){ // m1*m2 
				for(int k=0;k<nLength1;k++){ // arr1.T.row(arr1.col)*arr2.col
					r1=mRealArr1[i+k*mLength1];
					r2=mRealArr2[j+k*mLength2];

					i1=mImageArr1[i+k*mLength1];
					i2=mImageArr2[j+k*mLength2];

					_value1+=(r1*r2-i1*i2);
					_value2+=(i1*r2+r1*i2);
				}
			}
			else{ // m1*n2
				for(int k=0;k<nLength1;k++){ // arr1.T.row(arr1.col)*arr2.T.col(arr2.row)
					r1=mRealArr1[i+k*mLength1];
					r2=mRealArr2[j*mLength2+k];

					i1=mImageArr1[i+k*mLength1];
					i2=mImageArr2[j*mLength2+k];

					_value1+=(r1*r2-i1*i2);
					_value2+=(i1*r2+r1*i2);
				}
			}

			mRealArr3[i*mLen3+j]=_value1;
			mImageArr3[i*mLen3+j]=_value2;
		}
	}

	return status;
}

void __mcdiv(float *mRealArr1,float *mImageArr1,
			float *mRealArr2,float *mImageArr2,
			int nLength,int mLength,
			float *mRealArr3,float *mImageArr3){
	float *rArr=NULL;
	float *iArr=NULL;

	float real1=0;
	float image1=0;

	float real2=0;
	float image2=0;

	float real3=0;
	float image3=0;

	if(mRealArr3&&mImageArr3){
		rArr=mRealArr3;
		iArr=mImageArr3;
	}
	else{
		rArr=mRealArr1;
		iArr=mImageArr1;
	}

	for(int i=0;i<nLength;i++){
		for(int j=0;j<mLength;j++){
			real1=mRealArr1[i*mLength+j];
			image1=mImageArr1[i*mLength+j];

			real2=mRealArr2[i*mLength+j];
			image2=mImageArr2[i*mLength+j];

			__complexDiv(real1,image1,real2,image2,&real3,&image3);
			rArr[i*mLength+j]=real3;
			iArr[i*mLength+j]=image3;
		}
	}
}

void __mccut(float *mRealArr1,float *mImageArr1,
			int nLength,int mLength,
			int nIndex,int nLength1,
			int mIndex,int mLength1,
			float *mRealArr3,float *mImageArr3){
	float *rArr=NULL;
	float *iArr=NULL;
	int index=0;

	if(nIndex<0||
		nIndex>nLength-1||
		mIndex<0||
		mIndex>mLength-1||
		nIndex+nLength1>nLength||
		mIndex+mLength1>mLength){
		return;
	}

	if(mRealArr3&&mImageArr3){
		rArr=mRealArr3;
		iArr=mImageArr3;
	}
	else{
		rArr=mRealArr1;
		iArr=mImageArr1;
	}

	for(int i=nIndex;i<nLength1+nIndex;i++){
		for(int j=mIndex;j<mLength1+mIndex;j++){
			rArr[index]=mRealArr1[i*mLength+j];
			iArr[index]=mImageArr1[i*mLength+j];
			index++;
		}
	}
}

void __vcnew(int length,float *value,float **realArr,float **imageArr){
	float *rArr=NULL;
	float *iArr=NULL;

	float _value=0;

	if(value){
		_value=*value;
	}

	if(realArr){
		rArr=(float *)calloc(length, sizeof(float ));
		for(int i=0;i<length;i++){
			rArr[i]=_value;
		}

		*realArr=rArr;
	}

	if(imageArr){
		iArr=(float *)calloc(length, sizeof(float ));
		for(int i=0;i<length;i++){
			iArr[i]=_value;
		}

		*imageArr=iArr;
	}
}

void __vcangle(float *realArr1,float *imageArr1,int length,float *vArr1){
	float *arr=NULL;

	if(vArr1){
		arr=vArr1;
	}
	else{
		arr=imageArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=atan2f(imageArr1[i], realArr1[i]);
	}
}

void __vcabs(float *realArr1,float *imageArr1,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=imageArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=sqrtf(realArr1[i]*realArr1[i]+imageArr1[i]*imageArr1[i]);
	}
}

void __vcsquare(float *realArr1,float *imageArr1,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=imageArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=realArr1[i]*realArr1[i]+imageArr1[i]*imageArr1[i];
	}
}

// n*m complex=>n*m1 
void __mcabs(float *mRealArr,float *mImageArr,int nLength,int mLength,int axis,float *mArr2){
	float *mArr=NULL;

	int nLen=0;
	int mLen=0;

	if(mArr2){
		mArr=mArr2;
	}
	else{
		mArr=mImageArr;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	for(int i=0;i<nLen;i++){
		for(int j=0;j<mLen;j++){
			if(axis==0){
				mArr2[i+j*mLen]=sqrtf(mRealArr[i+j*mLen]*mRealArr[i+j*mLen]+
										mImageArr[i+j*mLen]*mImageArr[i+j*mLen]);
			}
			else{
				mArr2[i*mLen+j]=sqrtf(mRealArr[i*mLen+j]*mRealArr[i*mLen+j]+
										mImageArr[i*mLen+j]*mImageArr[i*mLen+j]);
			}
		}
	}
}

void __mcabs1(float *mRealArr,float *mImageArr,int nLength,int mLength,int axis,int cutLength,float *mArr2){
	float *mArr=NULL;

	int nLen=0;
	int mLen=0;

	if(mArr2){
		mArr=mArr2;
	}
	else{
		mArr=mImageArr;
	}

	if(axis==0){
		if(cutLength<0||cutLength>nLength){
			return;
		}

		nLen=cutLength;
		mLen=nLength;
	}
	else{
		if(cutLength<0||cutLength>mLength){
			return;
		}

		nLen=nLength;
		mLen=cutLength;
	}

	for(int i=0;i<nLen;i++){
		for(int j=0;j<mLen;j++){
			if(axis==0){
				mArr2[i+j*mLen]=sqrtf(mRealArr[i+j*mLen]*mRealArr[i+j*mLen]+
										mImageArr[i+j*mLen]*mImageArr[i+j*mLen]);
			}
			else{
				mArr2[i*mLen+j]=sqrtf(mRealArr[i*mLength+j]*mRealArr[i*mLength+j]+
										mImageArr[i*mLength+j]*mImageArr[i*mLength+j]);
			}
		}
	}
}

// n*m complex=>n*m1 
void __mcabs2(float *mRealArr,float *mImageArr,int nLength,int mLength,int mLength2,float *mArr2){
	float *mArr=NULL;

	if(mArr2){
		mArr=mArr2;
	}
	else{
		mArr=mImageArr;
	}

	if(mLength2<0||mLength2>mLength){
		return;
	}

	for(int i=0;i<nLength;i++){
		for(int j=0;j<mLength2;j++){
			mArr2[i*mLength2+j]=sqrtf(mRealArr[i*mLength+j]*mRealArr[i*mLength+j]+
										mImageArr[i*mLength+j]*mImageArr[i*mLength+j]);
		}
	}

}

void __mcsquare(float *mRealArr,float *mImageArr,int nLength,int mLength,int axis,float *mArr2){
	float *mArr=NULL;

	int nLen=0;
	int mLen=0;

	if(mArr2){
		mArr=mArr2;
	}
	else{
		mArr=mImageArr;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	for(int i=0;i<nLen;i++){
		for(int j=0;j<mLen;j++){
			if(axis==0){
				mArr2[i+j*mLen]=mRealArr[i+j*mLen]*mRealArr[i+j*mLen]+
										mImageArr[i+j*mLen]*mImageArr[i+j*mLen];
			}
			else{
				mArr2[i*mLen+j]=mRealArr[i*mLen+j]*mRealArr[i*mLen+j]+
										mImageArr[i*mLen+j]*mImageArr[i*mLen+j];
			}
		}
	}
}

void __mcsquare1(float *mRealArr,float *mImageArr,int nLength,int mLength,int axis,int cutLength,float *mArr2){
	float *mArr=NULL;

	int nLen=0;
	int mLen=0;

	if(mArr2){
		mArr=mArr2;
	}
	else{
		mArr=mImageArr;
	}

	if(axis==0){
		if(cutLength<0||cutLength>nLength){
			return;
		}

		nLen=cutLength;
		mLen=nLength;
	}
	else{
		if(cutLength<0||cutLength>mLength){
			return;
		}

		nLen=nLength;
		mLen=cutLength;
	}

	for(int i=0;i<nLen;i++){
		for(int j=0;j<mLen;j++){
			if(axis==0){
				mArr2[i+j*mLen]=mRealArr[i+j*mLen]*mRealArr[i+j*mLen]+
										mImageArr[i+j*mLen]*mImageArr[i+j*mLen];
			}
			else{
				mArr2[i*mLen+j]=mRealArr[i*mLength+j]*mRealArr[i*mLength+j]+
										mImageArr[i*mLength+j]*mImageArr[i*mLength+j];
			}
		}
	}
}

void __mcsquare2(float *mRealArr,float *mImageArr,int nLength,int mLength,int mLength2,float *mArr2){
	float *mArr=NULL;

	if(mArr2){
		mArr=mArr2;
	}
	else{
		mArr=mImageArr;
	}

	if(mLength2<0||mLength2>mLength){
		return;
	}

    #ifdef HAVE_OMP
    if(nLength<__kernelNum){
        omp_set_num_threads(nLength);
    }else{
        omp_set_num_threads(__kernelNum);
    }
    #endif

    if(nLength==1){
        for(int j=0;j<mLength2;j++){
            mArr2[j]=mRealArr[j]*mRealArr[j]+mImageArr[j]*mImageArr[j];
        }
    }else{
        #pragma omp parallel for
        for(int i=0;i<nLength;i++){
            for(int j=0;j<mLength2;j++){
                mArr2[i*mLength2+j]=mRealArr[i*mLength+j]*mRealArr[i*mLength+j]+
                                            mImageArr[i*mLength+j]*mImageArr[i*mLength+j];
            }
        }
    }
}

// add/sub/mul/div
void __vcmul(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *realArr3,float *imageArr3){

	float *rArr=NULL;
	float *iArr=NULL;

	if(!realArr3||!imageArr3){
		rArr=realArr1;
		iArr=imageArr1;
	}
	else{
		rArr=realArr3;
		iArr=imageArr3;
	}

	for(int i=0;i<length;i++){
		__complexMul(realArr1[i], imageArr1[i], realArr2[i], imageArr2[i], rArr+i, iArr+i);
	}
}

void __vcdiv(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *realArr3,float *imageArr3){
	float *rArr=NULL;
	float *iArr=NULL;

	if(!realArr3||!imageArr3){
		rArr=realArr1;
		iArr=imageArr1;
	}
	else{
		rArr=realArr3;
		iArr=imageArr3;
	}

	for(int i=0;i<length;i++){
		__complexDiv(realArr1[i], imageArr1[i], realArr2[i], imageArr2[i], rArr+i, iArr+i);
	}
}

void __vcadd(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *realArr3,float *imageArr3){
	float *rArr=NULL;
	float *iArr=NULL;

	if(!realArr3||!imageArr3){
		rArr=realArr1;
		iArr=imageArr1;
	}
	else{
		rArr=realArr3;
		iArr=imageArr3;
	}

	for(int i=0;i<length;i++){
		rArr[i]=realArr1[i]+realArr2[i];
		iArr[i]=imageArr1[i]+imageArr2[i];
	}
}

void __vcsub(float *realArr1,float *imageArr1,
			float *realArr2,float *imageArr2,int length,
			float *realArr3,float *imageArr3){
	float *rArr=NULL;
	float *iArr=NULL;

	if(!realArr3||!imageArr3){
		rArr=realArr1;
		iArr=imageArr1;
	}
	else{
		rArr=realArr3;
		iArr=imageArr3;
	}

	for(int i=0;i<length;i++){
		rArr[i]=realArr1[i]-realArr2[i];
		iArr[i]=imageArr1[i]-imageArr2[i];
	}
}

// debug vector/matrix相关
void __vcdebug(float *realArr,float *imageArr,int length,int type){
	if(type){
		printf("vector complex is:\n");

		printf("	");
		for(int i=0;i<length;i++){
			printf("%d:%f+j%f ,",i,realArr[i],imageArr[i]);
		}
	}
	else{
		printf("vector([");
		for(int i=0;i<length-1;i++){
			printf("%f+j%f, ",realArr[i],imageArr[i]);
		}
		printf("%f+j%f",realArr[length-1],imageArr[length-1]);
		printf("])\n");
	}

}

void __mcdebug(float *realArr,float *imageArr,int nLength,int mLength,int type){
	if(type){
		printf("matrix is:\n");

		for(int i=0;i<nLength;i++){
			printf("	%d:\n",i);
			printf("		");
			for(int j=0;j<mLength;j++){
				printf("%d:%f+j%f ,",j,realArr[i*mLength+j],imageArr[i*mLength+j]);
			}

			printf("\n\n");
		}
	}
	else{
		printf("matrix([");
		for(int i=0;i<nLength-1;i++){
			printf("[");

			for(int j=0;j<mLength-1;j++){
				printf("%f+j%f ,",realArr[i*mLength+j],imageArr[i*mLength+j]);
			}
			printf("%f++j%f",realArr[i*mLength+mLength-1],imageArr[i*mLength+mLength-1]);

			printf("],");
			printf("\n        ");
		}

		printf("[");
		for(int j=0;j<mLength-1;j++){
			printf("%f+j%f ,",realArr[(nLength-1)*mLength+j],imageArr[(nLength-1)*mLength+j]);
		}
		printf("%f+j%f",realArr[(nLength-1)*mLength+mLength-1],imageArr[(nLength-1)*mLength+mLength-1]);

		printf("]");
		printf("])\n");
	}
}

// power
void __vcpower1(float r,float t,float *vArr,int length,float *realArr1,float *imageArr1){

	for(int i=0;i<length;i++){
		float _r=0;

		_r=powf(r, vArr[i]);
		realArr1[i]=_r*cosf(t*vArr[i]);
		imageArr1[i]=_r*sinf(t*vArr[i]);
	}
}

/***
	b[0]*e^(j(M-1)w)+...+b[1]*e^(jw)+b[0];
	wArr1 角频率刻度
	vArr2 b/a系数
****/
void __vcpolyval(float *wArr1,int length1,float *vArr2,int length2,float *realArr3,float *imageArr3){

	for(int i=0;i<length1;i++){
		double _value1=0;
		double _value2=0;
		
		for(int j=0;j<length2;j++){ 
			_value1+=cos(wArr1[i]*(length2-1-j))*vArr2[j];
			_value2+=sin(wArr1[i]*(length2-1-j))*vArr2[j];
		}

		realArr3[i]=_value1;
		imageArr3[i]=_value2;
	}
}

void __complexMul(float real1,float image1,
				float real2,float image2,
				float *real3,float *image3){
	
	*real3=real1*real2-image1*image2;
	*image3=image1*real2+real1*image2;
}

void __complexDiv(float real1,float image1,
				float real2,float image2,
				float *real3,float *image3){
	float value=0;

	value=real2*real2+image2*image2;

	*real3=(real1*real2+image1*image2)/value;
	*image3=(image1*real2-real1*image2)/value;
}

float __complexMulM(float real1,float image1,
				float real2,float image2){
	float value=0;

	value=sqrtf(real1*real1+image1*image1)*sqrtf(real2*real2+image2*image2);

	return value;
}

float __complexDivM(float real1,float image1,
				float real2,float image2){
	float value=0;

	value=sqrtf(real1*real1+image1*image1)/sqrtf(real2*real2+image2*image2);

	return value;
}

float __complexPowM(float real,float image,int n){
	float value=0;

	value=sqrtf(real*real+image*image);
	value=powf(value, n);

	return value;
}



```

---

### Archivo: `./src/vector/flux_vectorOp.c`

```
// 

#include <string.h>
#include <math.h>

#include "flux_vector.h"
#include "flux_vectorOp.h"

// element math相关
// abs/ng/floor/ceil/round
void __vabs(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=fabsf(vArr1[i]);
	}
}

void __vng(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=-vArr1[i];
	}
}

void __vfloor(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=floorf(vArr1[i]);
	}
}

void __vceil(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=ceilf(vArr1[i]);
	}
}

void __vround(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=roundf(vArr1[i]);
	}
}


// cos/sin/tan/acos/asin/atan
void __vcos(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=cosf(vArr1[i]);
	}
}

void __vsin(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=sinf(vArr1[i]);
	}
}

void __vtan(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=tanf(vArr1[i]);
	}	
}	

void __vacos(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=acosf(vArr1[i]);
	}
}

void __vasin(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=asinf(vArr1[i]);
	}
}

void __vatan(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=atanf(vArr1[i]);
	}
}

// exp/exp2/pow/sqrt
void __vexp(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=expf(vArr1[i]);
	}
}

void __vexp2(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=exp2f(vArr1[i]);
	}
}

void __vpow(float *vArr1,float exp,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=powf(vArr1[i],exp);
	}
}

void __vsqrt(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=sqrtf(vArr1[i]);
	}
}


// log/log10/log2
void __vlog(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=logf(vArr1[i]);
	}
}

void __vlog10(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=log10f(vArr1[i]);
	}
}

void __vlog2(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=log2f(vArr1[i]);
	}
}

// log compress
void __vlog_compress(float *vArr1,float *gamma,float *base,int length,float *vArr2){
	float *arr=NULL;

	float _gamma=1.0;
	float _base=1.0;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	if(gamma){
		if(*gamma>0){
			_gamma=*gamma;
		}
	}

	if(base){
		if(*base>0){
			_base=*base;
		}
	}

	for(int i=0;i<length;i++){
		arr[i]=logf(vArr1[i]*_gamma+_base);
	}
}

void __vlog10_compress(float *vArr1,float *gamma,float *base,int length,float *vArr2){
	float *arr=NULL;

	float _gamma=1.0;
	float _base=1.0;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	if(gamma){
		if(*gamma>0){
			_gamma=*gamma;
		}
	}

	if(base){
		if(*base>0){
			_base=*base;
		}
	}

	for(int i=0;i<length;i++){
		arr[i]=log10f(vArr1[i]*_gamma+_base);
	}
}

void __vlog2_compress(float *vArr1,float *gamma,float *base,int length,float *vArr2){
	float *arr=NULL;

	float _gamma=1.0;
	float _base=1.0;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	if(gamma){
		if(*gamma>0){
			_gamma=*gamma;
		}
	}

	if(base){
		if(*base>0){
			_base=*base;
		}
	}

	for(int i=0;i<length;i++){
		arr[i]=log2f(vArr1[i]*_gamma+_base);
	}
}

// sinc=sin(pi*x)/x
void __vsinc(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		float _value=0;

		_value=vArr1[i]*M_PI;
		if(fabsf(_value)<1e-9){
			arr[i]=1;
		}
		else{
			arr[i]=sinf(_value)/_value;
		}
	}

}

void __vsinc_low(float *vArr1,int length,float cut,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	if(cut<=0||cut>=1){
		return;
	}

	for(int i=0;i<length;i++){
		arr[i]*=cut;
	}

	__vsinc(arr,length,arr);

	for(int i=0;i<length;i++){
		arr[i]*=cut;
	}
}

// sinc(1)-sinc(cut)
void __vsinc_high(float *vArr1,int length,float cut,float *vArr2){
	float *arr=NULL;
	float *_arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	if(cut<=0||cut>=1){
		return;
	}

	if(length%2==0){ // high coeff must odd
		printf("high coeff must odd!!!\n");
		return;
	}

	_arr=__vnew(length, NULL);

	__vsinc(vArr1,length,_arr); // sinc(1)
	__vsinc_low(vArr1,length,cut,vArr2); // sinc(cut)

	for(int i=0;i<length;i++){
		arr[i]=_arr[i]-vArr2[i];
	}

	free(_arr);
}

// sinc(cut2)-sinc(cut1)
void __vsinc_bandpass(float *vArr1,int length,float cut1,float cut2,float *vArr2){
	float *arr=NULL;
	float *_arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	if(cut1<=0||cut1>=1){
		return;
	}

	if(cut2<=0||cut2>=1){
		return;
	}

	if(cut2<=cut1){
		return;
	}

	_arr=__vnew(length, NULL);
	for(int i=0;i<length;i++){
		_arr[i]=vArr1[i]; // *cut2
	}
	__vsinc_low(_arr,length,cut2,_arr); // sinc(cut2)

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]; // *cut1
	}
	__vsinc_low(arr,length,cut1,arr); // sinc(cut1)

	for(int i=0;i<length;i++){
		arr[i]=_arr[i]-arr[i];
	}

	free(_arr);
}

// sinc(1)-sinc(cut2)+sinc(cut1)
void __vsinc_stop(float *vArr1,int length,float cut1,float cut2,float *vArr2){
	float *arr=NULL;

	float *_arr1=NULL;
	float *_arr2=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	if(cut1<=0||cut1>=1){
		return;
	}

	if(cut2<=0||cut2>=1){
		return;
	}

	if(cut2<=cut1){
		return;
	}

	if(length%2==0){ // high coeff must odd
		printf("stop coeff must odd!!!\n");
		return;
	}

	_arr1=__vnew(length, NULL);
	_arr2=__vnew(length, NULL);
	for(int i=0;i<length;i++){
		_arr1[i]=vArr1[i]; // *cut2
	}
	__vsinc_low(_arr1,length,cut2,_arr1); // sinc(cut2)

	for(int i=0;i<length;i++){
		_arr2[i]=vArr1[i]; // *cut1
	}
	__vsinc_low(_arr2,length,cut1,_arr2); // sinc(cut1)

	__vsinc(vArr1,length,arr); // sinc(1)
	for(int i=0;i<length;i++){
		arr[i]=arr[i]-_arr1[i]+_arr2[i];
	}

	free(_arr1);
	free(_arr2);
}

// 1/2阶 
void __vgradient(float *vArr1,int length,int edgeOrder,float *vArr2){

	if(length<2){
		return;
	}

	for(int i=0;i<length;i++){
		if(i==0){ // start f(k+1)-f(k)
			vArr2[i]=vArr1[i+1]-vArr1[i];
		}
		else if(i==length-1){ // f(k)-f(k-1)
			vArr2[i]=vArr1[i]-vArr1[i-1];
		}
		else{ // (f(k+1)-f(k-1))/2
			vArr2[i]=(vArr1[i+1]-vArr1[i-1])/2;
		}
	}

	if(edgeOrder>1){ // 2阶
		vArr2[0]-=(vArr2[1]-vArr2[0]);
		vArr2[length-1]+=(vArr2[length-1]-vArr2[length-2]);
	}
}

// interpolation
void __vinterp_linear(float *xArr1,float *yArr1,int length1,float *xArr2,int length2,float *yArr2){
	int index1=0;

	float x1=0;
	float y1=0;

	float x2=0;
	float y2=0;

	float value=0;

	for(int i=0;i<length2;i++){
		while(index1<length1-1&&xArr2[i]>xArr1[index1+1]){
			index1++;
		}

		if(index1<length1-1){
			x1=xArr1[index1];
			y1=yArr1[index1];

			x2=xArr1[index1+1];
			y2=yArr1[index1+1];

			value=y1+(xArr2[i]-x1)*(y2-y1)/(x2-x1);
			yArr2[i]=value;
		}
		else{
			yArr2[i]=yArr1[length1-1];
		}
	}
}

// pad type 0 'constant' 1 'refect' 2 'wrap'
void __vpad(float *vArr1,int length,
			int headLen,int tailLen,int type,
			float *value1,float *value2,
			float *vArr2){

}

void __mpad(float *mArr1,int nlength,int mLength,
			int headLen,int tailLen,int type,
			float *value1,float *value2,
			int axis,
			float *mArr2){

}

// constant
void __vpad_center1(float *vArr1,int vLength,
				int leftLength,int rightLength,
				float value1,float value2){
	for(int i=0;i<leftLength;i++){
		vArr1[i]=value1;
	}

	for(int i=leftLength+vLength;i<leftLength+rightLength+vLength;i++){
		vArr1[i]=value2;
	}
}

void __vpad_left1(float *vArr1,int vLength,int fLength,int value){
	for(int i=0;i<fLength;i++){
		vArr1[i]=value;
	}
}

void __vpad_right1(float *vArr1,int vLength,int fLength,int value){
	for(int i=vLength;i<fLength+vLength;i++){
		vArr1[i]=value;
	}
}

// reflect
void __vpad_center2(float *vArr1,int vLength,int leftLength,int rightLength){
	int startIndex=0;

	int leftIndex=0;
	int rightIndex=0;

	int flag=0; // 0 升 1降

	if(vLength<2){
		return;
	}

	startIndex=leftLength;
	leftIndex=1;
	for(int i=leftLength-1;i>=0;i--){
		vArr1[i]=vArr1[startIndex+leftIndex];

		if(!flag){ // 升
			if(leftIndex==vLength-1){
				flag=!flag;
				leftIndex--;
				continue;
			}
			else{
				leftIndex++;
			}
		}
		else{
			if(leftIndex==0){
				flag=!flag;
				leftIndex++;
				continue;
			}
			leftIndex--;
		}

		if(leftIndex==0||leftIndex==vLength-1){ // start||end
			flag=!flag;
		}
	}

	flag=1; // 降
	rightIndex=vLength-2;
	for(int i=leftLength+vLength;i<leftLength+rightLength+vLength;i++){
		vArr1[i]=vArr1[startIndex+rightIndex];

		if(!flag){ // 升
			if(rightIndex==vLength-1){
				flag=!flag;
				rightIndex--;
				continue;
			}
			else{
				rightIndex++;
			}
		}
		else{
			if(rightIndex==0){
				flag=!flag;
				rightIndex++;
				continue;
			}
			rightIndex--;
		}

		if(rightIndex==0||rightIndex==vLength-1){ // start||end
			flag=!flag;
		}
	}
}

void __vpad_left2(float *vArr1,int vLength,int leftLength){
	
	__vpad_center2(vArr1,vLength,leftLength,0);
}

void __vpad_right2(float *vArr1,int vLength,int rightLength){
	
	__vpad_center2(vArr1,vLength,0,rightLength);
}

// wrap
void __vpad_center3(float *vArr1,int vLength,int leftLength,int rightLength){
	int startIndex=0;

	int leftIndex=0;
	int rightIndex=0;

	if(vLength<2){
		return;
	}

	startIndex=leftLength;
	leftIndex=vLength-1;
	for(int i=leftLength-1;i>=0;i--){
		vArr1[i]=vArr1[startIndex+leftIndex];

		if(leftIndex==0){
			leftIndex=vLength-1;
		}
		else{
			leftIndex--;
		}
	}

	rightIndex=0;
	for(int i=leftLength+vLength;i<leftLength+rightLength+vLength;i++){
		vArr1[i]=vArr1[startIndex+rightIndex];

		if(rightIndex==vLength-1){
			rightIndex=0;
		}
		else{
			rightIndex++;
		}
	}
}

void __vpad_left3(float *vArr1,int vLength,int leftLength){
	
	__vpad_center3(vArr1,vLength,leftLength,0);
}

void __vpad_right3(float *vArr1,int vLength,int rightLength){

	__vpad_center3(vArr1,vLength,0,rightLength);
}

// symmetric 和reflect接近 min/max
void __vpad_center4(float *vArr1,int vLength,int leftLength,int rightLength){
	int startIndex=0;

	int leftIndex=0;
	int rightIndex=0;

	int flag=0; // 0 升 1降

	if(vLength<2){
		return;
	}

	startIndex=leftLength;
	leftIndex=0;
	for(int i=leftLength-1;i>=0;i--){
		vArr1[i]=vArr1[startIndex+leftIndex];

		if(!flag){ // 升
			if(leftIndex==vLength-1){
				flag=!flag;
				continue;
			}
			else{
				leftIndex++;
			}
		}
		else{
			if(leftIndex==0){
				flag=!flag;
				continue;
			}
			leftIndex--;
		}
	}

	flag=1; // 降
	rightIndex=vLength-1;
	for(int i=leftLength+vLength;i<leftLength+rightLength+vLength;i++){
		vArr1[i]=vArr1[startIndex+rightIndex];

		if(!flag){ // 升
			if(rightIndex==vLength-1){
				flag=!flag;
				continue;
			}
			else{
				rightIndex++;
			}
		}
		else{
			if(rightIndex==0){
				flag=!flag;
				continue;
			}
			rightIndex--;
		}
	}
}

void __vpad_left4(float *vArr1,int vLength,int leftLength){

	__vpad_center4(vArr1,vLength,leftLength,0);
}

void __vpad_right4(float *vArr1,int vLength,int rightLength){

	__vpad_center4(vArr1,vLength,0,rightLength);
}

// edge
void __vpad_center5(float *vArr1,int vLength,int leftLength,int rightLength){
	for(int i=0;i<leftLength;i++){
		vArr1[i]=vArr1[leftLength];
	}

	for(int i=leftLength+vLength;i<leftLength+rightLength+vLength;i++){
		vArr1[i]=vArr1[leftLength+vLength-1];
	}
}

void __vpad_left5(float *vArr1,int vLength,int leftLength){
	for(int i=0;i<leftLength;i++){
		vArr1[i]=vArr1[leftLength];
	}
}

void __vpad_right5(float *vArr1,int vLength,int rightLength){
	for(int i=vLength;i<vLength+rightLength;i++){
		vArr1[i]=vArr1[vLength-1];
	}
}










```

---

### Archivo: `./src/vector/flux_vector.c`

```
// 

#include <string.h>
#include <math.h>

#ifdef HAVE_ACCELERATE
#include <Accelerate/Accelerate.h>
#elif defined HAVE_OPENBLAS
#include <cblas.h>
#elif defined HAVE_MKL
#include <mkl.h>
//#elif defined HAVE_CUDABLAS
//#include <cublas_v2.h>
#endif

#include "flux_vector.h"

static float __arr_max(float *vArr,int length);
static void __mREZ(float *mArr1,int nLength,int mLength,int axis,float *vArr3,float (*func)(float *,int ));
static void __vunwrap1(float **vArr1,int length);

// 针对 type 0即符合乘法
void __mdot(float *mArr1,float *mArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			float *mArr3){
	if(mLength1!=nLength2){
		return;
	}

    #if (defined HAVE_ACCELERATE) || (defined HAVE_OPENBLAS) || (defined HAVE_MKL)
    memset(mArr3, 0, nLength1 * mLength2 * sizeof(float));
    cblas_sgemm(CblasRowMajor, CblasNoTrans, CblasNoTrans,
                nLength1, mLength2,
                mLength1, 1,
                mArr1, mLength1,
                mArr2, mLength2,
                1, mArr3, mLength2);
    #else
	for(int i=0;i<nLength1;i++){
		for(int j=0;j<mLength2;j++){
			double _value=0;

			for(int k=0;k<mLength1;k++){ // arr1.row*arr2.col
				_value+=mArr1[i*mLength1+k]*mArr2[j+k*mLength2];
			}

			mArr3[i*mLength2+j]=_value;
		}
	}
    #endif
}

// 针对 type 1即m2转置符合乘法
void __mdot1(float *mArr1,float *mArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			float *mArr3){
	if(mLength1!=mLength2){
		return;
	}

    #if (defined HAVE_ACCELERATE) || (defined HAVE_OPENBLAS) || (defined HAVE_MKL)
    memset(mArr3, 0, nLength1 * nLength2 * sizeof(float));
    cblas_sgemm(CblasRowMajor, CblasNoTrans, CblasTrans,
                nLength1, nLength2,
                mLength1, 1,
                mArr1, mLength1,
                mArr2, mLength2,
                1, mArr3, nLength2);
    //#elif defined HAVE_CUDABLAS
    //    __mdot1_cudablas(mArr1, mArr2, nLength1, mLength1, nLength2, mLength2, mArr3);
    #else
	for(int i=0;i<nLength1;i++){
		for(int j=0;j<nLength2;j++){
			double _value=0;

			for(int k=0;k<mLength1;k++){ // arr1.row*arr2.row
				_value+=mArr1[i*mLength1+k]*mArr2[j*mLength2+k];
			}

			mArr3[i*nLength2+j]=_value;
		}
	}
    #endif
}

//#ifdef HAVE_CUDABLAS
//void __mdot1_cudablas(float* mArr1, float*mArr2,
//			int nLength1,int mLength1,
//			int nLength2,int mLength2,
//			float *mArr3) {
//	struct timeval tv;
//    long t1=0,t2=0;
//    gettimeofday(&tv, NULL);
//    t1=tv.tv_sec*1000+tv.tv_usec/1000;
//
//    float alpha = 1;
//    float beta = 1;
//
//    // 在 GPU 上分配内存
//    float *d_A, *d_B, *d_C;
//    cudaMalloc(&d_A, nLength1 * mLength1 * sizeof(float));
//    cudaMalloc(&d_B, nLength2 * mLength2 * sizeof(float));
//    cudaMalloc(&d_C, nLength1 * nLength2 * sizeof(float));
//
//    printf("%d,%d,%d,%d\n", nLength1, mLength1, nLength2, mLength2);
//
//    // 将数据从 CPU 复制到 GPU
//    cudaMemcpy(d_A, mArr1, nLength1 * mLength1 * sizeof(float), cudaMemcpyHostToDevice);
//    cudaMemcpy(d_B, mArr2, nLength2 * mLength2 * sizeof(float), cudaMemcpyHostToDevice);
//    cudaMemcpy(d_C, mArr3, nLength1 * nLength2 * sizeof(float), cudaMemcpyHostToDevice);
//
//    // 初始化 cuBLAS
//    cublasHandle_t handle;
//    cublasCreate(&handle);
//
//    cublasSgemm(handle, CUBLAS_OP_N, CUBLAS_OP_T, nLength2, nLength1, nLength2, &alpha, d_B, mLength2, d_A, nLength1, &beta, d_C, nLength2);
//
//    // 将结果从 GPU 复制回 CPU
//    cudaMemcpy(mArr3, d_C, nLength1 * nLength2 * sizeof(float), cudaMemcpyDeviceToHost);
//
//    // 清理 cuBLAS 资源和 GPU 内存
//    cublasDestroy(handle);
//    cudaFree(d_A);
//    cudaFree(d_B);
//    cudaFree(d_C);
//    gettimeofday(&tv, NULL);
//    t2=tv.tv_sec*1000+tv.tv_usec/1000;
//    float time = (t2-t1)/1000.0;
//    printf("cost time: %0.10f\n",time);
//}
//#endif

/***
	n1*m1 n2*m2 => n3*m3
	type
		0 n1*m2 m1==n2
		1 n1*n2 m1==m2
		2 m1*m2 n1==n2
		3 m1*n2 n1==m2
	不能in place操作
	return 0 sucess 1 error
****/
int __mdot2(float *mArr1,float *mArr2,
			int nLength1,int mLength1,
			int nLength2,int mLength2,
			int *type,
			float *mArr3){
	int status=0;

	int nLen3=0;
	int mLen3=0;

	int _type=0;

	if(type){
		_type=*type;
	}

	if(_type==0){ // n1*m2
		nLen3=nLength1;
		mLen3=mLength2;
		if(mLength1!=nLength2){
			return -1;
		}
	}
	else if(_type==1){ // n1*n2
		nLen3=nLength1;
		mLen3=nLength2;
		if(mLength1!=mLength2){
			return -1;
		}
	}
	else if(_type==2){ // m1*m2
		nLen3=mLength1;
		mLen3=mLength2;
		if(nLength1!=nLength2){
			return -1;
		}
	}
	else{ // m1*n2
		nLen3=mLength1;
		mLen3=nLength2;
		if(nLength1!=mLength2){
			return -1;
		}
	}

	for(int i=0;i<nLen3;i++){
		for(int j=0;j<mLen3;j++){
			double _value=0;

			if(_type==0){ // n1*m2
				for(int k=0;k<mLength1;k++){ // arr1.row*arr2.col
					_value+=mArr1[i*mLength1+k]*mArr2[j+k*mLength2];
				}
			}
			else if(_type==1){ // n1*n2 
				for(int k=0;k<mLength1;k++){ // arr1.row*arr2.T.col(arr2.row)
					_value+=mArr1[i*mLength1+k]*mArr2[j*mLength2+k];
				}
			}
			else if(_type==2){ // m1*m2 
				for(int k=0;k<nLength1;k++){ // arr1.T.row(arr1.col)*arr2.col
					_value+=mArr1[i+k*mLength1]*mArr2[j+k*mLength2];
				}
			}
			else{ // m1*n2
				for(int k=0;k<nLength1;k++){ // arr1.T.row(arr1.col)*arr2.T.col(arr2.row)
					_value+=mArr1[i+k*mLength1]*mArr2[j*mLength2+k];
				}
			}

			mArr3[i*mLen3+j]=_value;
		}
	}

	return status;
}

void __msub(float *mArr1,float *mArr2,int nLength,int mLength,float *mArr3){

	for(int i=0;i<nLength*mLength;i++){
		mArr3[i]=mArr1[i]-mArr2[i];
	}
}

/***
	A n*m
	1*m/n*1=>0/1/ => axis 0/1
****/
void __mmul_vector(float *mArr1,float *vArr,int type,int nLength,int mLength,int axis,float *mArr3){
	float *arr=NULL;

	int nLen=0;
	int mLen=0;

	if(mArr3){
		arr=mArr3;
	}
	else{
		arr=mArr1;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	for(int i=0;i<nLen;i++){
		for(int j=0;j<mLen;j++){
			if(axis==0){ // 1*m
				arr[i+j*mLength]=mArr1[i+j*mLength]*(type==0?vArr[j]:vArr[i]);
			}
			else{ // n*1
				arr[i*mLength+j]=mArr1[i*mLength+j]*(type?vArr[j]:vArr[i]);
			}
		}
	}
}

void __mdiv_vector(float *mArr1,float *vArr,int type,int nLength,int mLength,int axis,float *mArr3){
	float *arr=NULL;

	int nLen=0;
	int mLen=0;

	if(mArr3){
		arr=mArr3;
	}
	else{
		arr=mArr1;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	for(int i=0;i<nLen;i++){
		for(int j=0;j<mLen;j++){
			if(axis==0){ // 1*m
				if(mArr1[i+j*mLength]){
					arr[i+j*mLength]=mArr1[i+j*mLength]/(type==0?vArr[j]:vArr[i]);
				}
				else{
					arr[i+j*mLength]=0;
				}
			}
			else{ // n*1
				if(mArr1[i*mLength+j]){
					arr[i*mLength+j]=mArr1[i*mLength+j]/(type?vArr[j]:vArr[i]);
				}
				else{
					arr[i*mLength+j]=0;
				}
			}
		}
	}
}

void __madd_vector(float *mArr1,float *vArr,int type,int nLength,int mLength,int axis,float *mArr3){
	float *arr=NULL;

	int nLen=0;
	int mLen=0;

	if(mArr3){
		arr=mArr3;
	}
	else{
		arr=mArr1;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	for(int i=0;i<nLen;i++){
		for(int j=0;j<mLen;j++){
			if(axis==0){ // 1*m
				arr[i+j*mLength]=mArr1[i+j*mLength]+(type==0?vArr[j]:vArr[i]);
			}
			else{ // n*1
				arr[i*mLength+j]=mArr1[i*mLength+j]+(type?vArr[j]:vArr[i]);
			}
		}
	}
}

void __msub_vector(float *mArr1,float *vArr,int type,int nLength,int mLength,int axis,float *mArr3){
	float *arr=NULL;

	int nLen=0;
	int mLen=0;

	if(mArr3){
		arr=mArr3;
	}
	else{
		arr=mArr1;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	for(int i=0;i<nLen;i++){
		for(int j=0;j<mLen;j++){
			if(axis==0){ // 1*m
				arr[i+j*mLength]=mArr1[i+j*mLength]-(type==0?vArr[j]:vArr[i]);
			}
			else{ // n*1
				arr[i*mLength+j]=mArr1[i*mLength+j]-(type?vArr[j]:vArr[i]);
			}
		}
	}
}

void __mmul_value(float *mArr1,float value,int nLength,int mLength,float *mArr3){
	float *mArr=NULL;

	if(mArr3){
		mArr=mArr3;
	}
	else{
		mArr=mArr1;
	}

	for(int i=0;i<nLength;i++){
		for(int j=0;j<mLength;j++){
			mArr[i*mLength+j]=mArr1[i*mLength+j]*value;
		}
	}
}

/***
	axis 0 row 1 col -1/other all
****/
void __msum(float *mArr1,int nLength,int mLength,int axis,float *vArr3){
	int nLen=0;
	int mLen=0;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			double _value=0;

			for(int j=0;j<mLen;j++){
				if(axis==0){ // col遍历
					_value+=mArr1[i+j*mLength];
				}
				else{ // row 遍历
					_value+=mArr1[i*mLength+j];
				}
			}

			vArr3[i]=_value;
		}
	}
	else{ 
		vArr3[0]=__vsum(mArr1, nLength*mLength);
	}
}

void __mmin(float *mArr1,int nLength,int mLength,int axis,float *vArr3,int *indexArr3){
	float min=0;
	int index=0;

	int nLen=0;
	int mLen=0;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			for(int j=0;j<mLen;j++){
				if(axis==0){ // col遍历
					if(j==0){
						vArr3[i]=mArr1[i+j*mLength];
						if(indexArr3){
							indexArr3[i]=j;	
						}
					}
					else{
						if(vArr3[i]>mArr1[i+j*mLength]){
							vArr3[i]=mArr1[i+j*mLength];
							if(indexArr3){
								indexArr3[i]=j;
							}
						}
					}
					
				}
				else{ // row遍历
					if(j==0){
						vArr3[i]=mArr1[i*mLength+j];
						if(indexArr3){
							indexArr3[i]=j;
						}
					}
					else{
						if(vArr3[i]>mArr1[i*mLength+j]){
							vArr3[i]=mArr1[i*mLength+j];
							if(indexArr3){
								indexArr3[i]=j;
							}
						}
					}
				}
			}
		}
	}
	else{ 
		index=__vmin(mArr1, nLength*mLength,&min);
		vArr3[0]=min;
		if(indexArr3){
			indexArr3[0]=index;
		}
	}
}

void __mmax(float *mArr1,int nLength,int mLength,int axis,float *vArr3,int *indexArr3){
	float max=0;
	int index=0;

	int nLen=0;
	int mLen=0;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			for(int j=0;j<mLen;j++){
				if(axis==0){ // col遍历
					if(j==0){
						vArr3[i]=mArr1[i+j*mLength];
						if(indexArr3){
							indexArr3[i]=j;	
						}
					}
					else{
						if(vArr3[i]<mArr1[i+j*mLength]){
							vArr3[i]=mArr1[i+j*mLength];
							if(indexArr3){
								indexArr3[i]=j;
							}
						}
					}
					
				}
				else{ // row遍历
					if(j==0){
						vArr3[i]=mArr1[i*mLength+j];
						if(indexArr3){
							indexArr3[i]=j;
						}
					}
					else{
						if(vArr3[i]<mArr1[i*mLength+j]){
							vArr3[i]=mArr1[i*mLength+j];
							if(indexArr3){
								indexArr3[i]=j;
							}
						}
					}
				}
			}
		}
	}
	else{ 
		index=__vmax(mArr1, nLength*mLength,&max);
		vArr3[0]=max;
		if(indexArr3){
			indexArr3[0]=index;
		}
	}
}

void __mmean(float *mArr1,int nLength,int mLength,int axis,float *vArr3){

	if(!vArr3){
		return;
	}

	__msum(mArr1,nLength,mLength,axis,vArr3);
	if(axis==0||axis==1){
		if(axis==0){
			__vdiv_value(vArr3, nLength, mLength, vArr3);
		}
		else{ // axis==1
			__vdiv_value(vArr3, mLength, nLength, vArr3);
		}
	}
	else{
		vArr3[0]/=(nLength*mLength);
	}
}

// 转__v系列
void __mmedian(float *mArr1,int nLength,int mLength,int axis,float *vArr3){
	int nLen=0;
	int mLen=0;

	float *vArr=NULL;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;

			vArr=__vnew(mLen, NULL);
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			if(axis==0){
				for(int j=0;j<mLen;j++){
					if(axis==0){ // col遍历
						vArr[j]=mArr1[i+j*mLength];
					}
				}
			}
			else{
				vArr=mArr1+i*mLength;
			}

			vArr3[i]=__vmedian(vArr, mLen);
		}

		if(axis==0){
			free(vArr);
		}
	}
}

void __mvar(float *mArr1,int nLength,int mLength,int axis,int type,float *vArr3){
	int nLen=0;
	int mLen=0;

	float *vArr=NULL;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;

			vArr=__vnew(mLen, NULL);
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			if(axis==0){
				for(int j=0;j<mLen;j++){
					if(axis==0){ // col遍历
						vArr[j]=mArr1[i+j*mLength];
					}
				}
			}
			else{
				vArr=mArr1+i*mLength;
			}

			vArr3[i]=__vvar(vArr, mLen, type);
		}

		if(axis==0){
			free(vArr);
		}
	}
}

void __mstd(float *mArr1,int nLength,int mLength,int axis,int type,float *vArr3){
	int nLen=0;
	int mLen=0;

	float *vArr=NULL;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;

			vArr=__vnew(mLen, NULL);
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			if(axis==0){
				for(int j=0;j<mLen;j++){
					if(axis==0){ // col遍历
						vArr[j]=mArr1[i+j*mLength];
					}
				}
			}
			else{
				vArr=mArr1+i*mLength;
			}

			vArr3[i]=__vstd(vArr, mLen, type);
		}

		if(axis==0){
			free(vArr);
		}
	}
}

void __mcov(float *mArr1,float *mArr2,int nLength,int mLength,int axis,int type,float *vArr3){
	int nLen=0;
	int mLen=0;

	float *vArr1=NULL;
	float *vArr2=NULL;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;

			vArr1=__vnew(mLen, NULL);
			vArr2=__vnew(mLen, NULL);
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			if(axis==0){
				for(int j=0;j<mLen;j++){
					if(axis==0){ // col遍历
						vArr1[j]=mArr1[i+j*mLength];
						vArr2[j]=mArr2[i+j*mLength];
					}
				}
			}
			else{
				vArr1=mArr1+i*mLength;
				vArr2=mArr2+i*mLength;
			}

			vArr3[i]=__vcov(vArr1,vArr2, mLen, type);
		}

		if(axis==0){
			free(vArr1);
			free(vArr2);
		}
	}
}

void __mcorrcoef(float *mArr1,float *mArr2,int nLength,int mLength,int axis,float *vArr3){
	int nLen=0;
	int mLen=0;

	float *vArr1=NULL;
	float *vArr2=NULL;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;

			vArr1=__vnew(mLen, NULL);
			vArr2=__vnew(mLen, NULL);
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			if(axis==0){
				for(int j=0;j<mLen;j++){
					if(axis==0){ // col遍历
						vArr1[j]=mArr1[i+j*mLength];
						vArr2[j]=mArr2[i+j*mLength];
					}
				}
			}
			else{
				vArr1=mArr1+i*mLength;
				vArr2=mArr2+i*mLength;
			}

			vArr3[i]=__vcorrcoef(vArr1,vArr2, mLen);
		}

		if(axis==0){
			free(vArr1);
			free(vArr2);
		}
	}
}

static void __mREZ(float *mArr1,int nLength,int mLength,int axis,float *vArr3,float (*func)(float *,int )){
	int nLen=0;
	int mLen=0;

	float *vArr=NULL;

	if(!vArr3){
		return;
	}

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;

			vArr=__vnew(mLen, NULL);
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			if(axis==0){
				for(int j=0;j<mLen;j++){
					if(axis==0){ // col遍历
						vArr[j]=mArr1[i+j*mLength];
					}
				}
			}
			else{
				vArr=mArr1+i*mLength;
			}

			vArr3[i]=func(vArr, mLen);
		}

		if(axis==0){
			free(vArr);
		}
	}
}

void __mrms(float *mArr1,int nLength,int mLength,int axis,float *vArr3){
	
	__mREZ(mArr1,nLength,mLength,axis,vArr3,__vrms);
}

void __menergy(float *mArr1,int nLength,int mLength,int axis,float *vArr3){

	__mREZ(mArr1,nLength,mLength,axis,vArr3,__venergy);
}

void __mzcr(float *mArr1,int nLength,int mLength,int axis,float *vArr3){

	__mREZ(mArr1,nLength,mLength,axis,vArr3,__vzcr);
}

void __munwrap(float *mArr1,int nLength,int mLength,int axis){
	int nLen=0;
	int mLen=0;

	float **vArr1=NULL;

	if(axis==0||axis==1){
		if(axis==0){
			nLen=mLength;
			mLen=nLength;

			vArr1=(float **)calloc(mLen, sizeof(float *));
		}
		else{
			nLen=nLength;
			mLen=mLength;
		}

		for(int i=0;i<nLen;i++){
			if(axis==0){
				for(int j=0;j<mLen;j++){
					if(axis==0){ // col遍历
						vArr1[j]=mArr1+(i+j*mLength);
					}
				}

				__vunwrap1(vArr1, mLen);
			}
			else{
				__vunwrap(mArr1+i*mLength, mLen, NULL);
			}
		}

		if(axis==0){
			free(vArr1);
		}
	}
}

float __vdot(float *vArr1,float *vArr2,int length){
	float value=0;

	for(int i=0;i<length;i++){
		value+=vArr1[i]*vArr2[i];
	}

	return value;
}

void __vmul(float *vArr1,float *vArr2,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]*vArr2[i];
	}
}

void __vdiv(float *vArr1,float *vArr2,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]/vArr2[i];
	}
}

void __vadd(float *vArr1,float *vArr2,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]+vArr2[i];
	}
}

void __vsub(float *vArr1,float *vArr2,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]-vArr2[i];
	}
}

void __vmul_value(float *vArr1,float value,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]*value;
	}
}

void __vdiv_value(float *vArr1,float value,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]/value;
	}
}

void __vadd_value(float *vArr1,float value,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]+value;
	}
}

void __vsub_value(float *vArr1,float value,int length,float *vArr3){
	float *arr=NULL;

	if(vArr3){
		arr=vArr3;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]-value;
	}
}

float __vnorm(float *vArr1,int length){
	float value=0;

	for(int i=0;i<length;i++){
		value+=vArr1[i]*vArr1[i];
	}
	value=sqrtf(value);

	return value;
}

// type 0 p 1/2/3... 1 Inf 2 -Inf
void __mnormalize(float *mArr1,int nLength,int mLength,int axis,int type,float p,float *mArr3){
	float *arr=NULL;

	int nLen=0;
	int mLen=0;

	float *vArr=NULL;

	if(mArr3){
		arr=mArr3;
	}
	else{
		arr=mArr1;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	vArr=__vnew(nLen, NULL);

	// 1. cal vArr
	for(int i=0;i<nLen;i++){
		vArr[i]=0;
		for(int j=0;j<mLen;j++){
			float _value=0;

			if(axis==0){ // 1*m
				_value=mArr1[i+j*mLength];
			}
			else{ // n*1
				_value=mArr1[i*mLength+j];
			}

			_value=fabsf(_value);
			if(type==0){ // P-L范式
				if(p==1.0){
					vArr[i]+=_value;
				}
				else if(p==2.0){
					vArr[i]+=_value*_value;
				}
				else{
					vArr[i]+=powf(_value, p);
				}
			}
			else if(type==1){ // max 
				if(j==0){
					vArr[i]=_value;
				}
				else{
					if(vArr[i]<_value){
						vArr[i]=_value;
					}
				}
			}
			else{ // min
				if(j==0){
					vArr[i]=_value;
				}
				else{
					if(vArr[i]>_value){
						vArr[i]=_value;
					}
				}
			}
		}

		if(type==0){ // P-L
			if(p!=1.0){
				if(p==2.0){
					vArr[i]=sqrtf(vArr[i]);
				}
				else{
					vArr[i]=powf(vArr[i], 1/p);
				}
			}
		}
	}

	// 2. div
	for(int i=0;i<nLen;i++){
		if(vArr[i]!=0){
			for(int j=0;j<mLen;j++){
				if(axis==0){ // 1*m
					arr[i+j*mLength]=mArr1[i+j*mLength]/vArr[i];
				}
				else{ // n*1
					arr[i*mLength+j]=mArr1[i*mLength+j]/vArr[i];
				}
			}
		}
	}

	free(vArr);
}

void __mnorm(float *mArr1,int nLength,int mLength,int axis,int type,float p,float *vArr2){
	float *arr=NULL;

	int nLen=0;
	int mLen=0;

	float *vArr=NULL;

	arr=mArr1;
	vArr=vArr2;

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	// 1. cal vArr
	for(int i=0;i<nLen;i++){
		vArr[i]=0;
		for(int j=0;j<mLen;j++){
			float _value=0;

			if(axis==0){ // 1*m
				_value=mArr1[i+j*mLength];
			}
			else{ // n*1
				_value=mArr1[i*mLength+j];
			}

			_value=fabsf(_value);
			if(type==0){ // P-L范式
				if(p==1.0){
					vArr[i]+=_value;
				}
				else if(p==2.0){
					vArr[i]+=_value*_value;
				}
				else{
					vArr[i]+=powf(_value, p);
				}
			}
			else if(type==1){ // max 
				if(j==0){
					vArr[i]=_value;
				}
				else{
					if(vArr[i]<_value){
						vArr[i]=_value;
					}
				}
			}
			else{ // min
				if(j==0){
					vArr[i]=_value;
				}
				else{
					if(vArr[i]>_value){
						vArr[i]=_value;
					}
				}
			}
		}

		if(type==0){ // P-L
			if(p!=1.0){
				if(p==2.0){
					vArr[i]=sqrtf(vArr[i]);
				}
				else{
					vArr[i]=powf(vArr[i], 1/p);
				}
			}
		}
	}
}

// 向量归一化 type 0 p 1/2/3... 1 Inf 2 -Inf
void __vnormalize(float *vArr1,int length,int type,float p,float *vArr2){
	float *arr=NULL;

	float value=0;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		float _value=0;

		_value=vArr1[i];
		_value=fabsf(_value);
		if(type==0){ // P-L
			if(p==1.0){
				value+=_value;
			}
			else if(p==2.0){
				value+=_value*_value;
			}
			else{
				value+=powf(_value, p);
			}
		}
		else if(type==1){ // max
			if(i==0){
				value=_value;
			}
			else{
				if(value<_value){
					value=_value;
				}
			}
		}
		else{ // min
			if(i==0){
				value=_value;
			}
			else{
				if(value>_value){
					value=_value;
				}
			}
		}
	}

	if(type==0){ // P-L
		if(p!=1.0){
			if(p==2.0){
				value=sqrtf(value);
			}
			else{
				value=powf(value, 1/p);
			}
		}
	}

	if(value!=0){
		for(int i=0;i<length;i++){
			arr[i]=vArr1[i]/value;
		}
	}
}

// 各种scale
// 不适用稀疏数据
void __vminmaxscale(float *vArr1,int length,float *vArr2){
	float min=0;
	float max=0;

	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	__vmin(vArr1, length, &min);
	__vmax(vArr1, length, &max);
	if(max>min){
		for(int i=0;i<length;i++){
			arr[i]=(vArr1[i]-min)/(max-min);
		}
	}
}

// 通用数据标准化 均值0方差1 不适用用稀疏数据
void __vstandscale(float *vArr1,int length,int type,float *vArr2){
	float mean=0;
	float std=0;

	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	mean=__vmean(vArr1, length);
	std=__vstd(vArr1, length, type);
	if(std){
		for(int i=0;i<length;i++){
			arr[i]=(vArr1[i]-mean)/std;
		}
	}
}

// 使用稀疏矩阵
void __vmaxabsscale(float *vArr1,int length,float *vArr2){
	float max=0;

	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	__vmaxabs(vArr1, length, &max);
	if(max){
		for(int i=0;i<length;i++){
			arr[i]=vArr1[i]/max;
		}
	}
}

void __vrobustscale(float *vArr1,int length,float *vArr2){
	float q1=0;
	float q3=0;
	float q2=0;

	int index=0;
	int mod=0;

	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	index=(length+1)/2-1;
	mod=(length+1)%2;
	if(index>=0){
		if(!mod){ // 整除
			q2=vArr1[index];
		}
		else{
			q2=(vArr1[index]+vArr1[index+1])/2;
		}
	}

	index=(length+1)/4-1;
	mod=(length+1)%4;
	if(index>=0){
		if(!mod){ // 整除
			q1=vArr1[index];
		}
		else{
			q1=(vArr1[index]+vArr1[index+1])/2;
		}
	}

	index=(length+1)*3/4-1;
	mod=(length+1)*3%4;
	if(index>=0){
		if(!mod){ // 整除
			q3=vArr1[index];
		}
		else{
			q3=(vArr1[index]+vArr1[index+1])/2;
		}
	}

	if(q3>q1){
		for(int i=0;i<length;i++){
			arr[i]=(vArr1[i]-q2)/(q3-q1);
		}
	}
}

void __vcenterscale(float *vArr1,int length,float *vArr2){
	float mean=0;

	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	mean=__vmean(vArr1, length);
	for(int i=0;i<length;i++){
		arr[i]=vArr1[i]-mean;
	}
}

void __vmeanscale(float *vArr1,int length,float *vArr2){
	float min=0;
	float max=0;

	float mean=0;

	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	__vmin(vArr1, length, &min);
	__vmax(vArr1, length, &max);

	mean=__vmean(vArr1, length);
	if(max>min){
		for(int i=0;i<length;i++){
			arr[i]=(vArr1[i]-mean)/(max-min);
		}
	}
}

void __varctanscale(float *vArr1,int length,float *vArr2){
	float *arr=NULL;

	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=atanf(vArr1[i])/(M_PI/2);
	}
}

float __vsum(float *vArr1,int length){
	double value=0;

	for(int i=0;i<length;i++){
		value+=vArr1[i];
	}
	
	return value;
}

int __vsumi(int *vArr1,int length){
	int value=0;

	for(int i=0;i<length;i++){
		value+=vArr1[i];
	}
	
	return value;
}

int __vmin(float *vArr1,int length,float *value){
	int index=0;
	float min=0;

	if(!vArr1||!length){
		return -1;
	}

	min=vArr1[0];
	for(int i=1;i<length;i++){
		if(min>vArr1[i]){
			min=vArr1[i];
			index=i;
		}
	}

	if(value){
		*value=min;
	}

	return index;
}

int __vmax(float *vArr1,int length,float *value){
	int index=0;
	float max=0;

	if(!vArr1||!length){
		return -1;
	}

	max=vArr1[0];
	for(int i=1;i<length;i++){
		if(max<vArr1[i]){
			max=vArr1[i];
			index=i;
		}
	}

	if(value){
		*value=max;
	}

	return index;
}

int __vmini(int *vArr1,int length,int *value){
	int index=0;
	int min=0;

	if(!vArr1||!length){
		return -1;
	}

	min=vArr1[0];
	for(int i=1;i<length;i++){
		if(min>vArr1[i]){
			min=vArr1[i];
			index=i;
		}
	}

	if(value){
		*value=min;
	}

	return index;
}

int __vmaxi(int *vArr1,int length,int *value){
	int index=0;
	int max=0;

	if(!vArr1||!length){
		return -1;
	}

	max=vArr1[0];
	for(int i=1;i<length;i++){
		if(max<vArr1[i]){
			max=vArr1[i];
			index=i;
		}
	}

	if(value){
		*value=max;
	}

	return index;
}

int __vminabs(float *vArr1,int length,float *value){
	int index=0;
	float min=0;

	if(!vArr1||!length){
		return -1;
	}

	min=fabs(vArr1[0]);
	for(int i=1;i<length;i++){
		if(min>fabs(vArr1[i])){
			min=fabs(vArr1[i]);
			index=i;
		}
	}

	if(value){
		*value=min;
	}

	return index;
}

int __vmaxabs(float *vArr1,int length,float *value){
	int index=0;
	float max=0;

	if(!vArr1||!length){
		return -1;
	}

	max=fabs(vArr1[0]);
	for(int i=1;i<length;i++){
		if(max<fabs(vArr1[i])){
			max=fabs(vArr1[i]);
			index=i;
		}
	}

	if(value){
		*value=max;
	}

	return index;
}

float __vmean(float *vArr1,int length){
	float value=0;

	for(int i=0;i<length;i++){
		value+=vArr1[i];
	}
	value/=length;

	return value;
}

float __vmedian(float *vArr1,int length){
	float value=0;
	float *vArr2=NULL;

	int start=0;
	int len=0;

	if(!vArr1||!length){
		return 0;
	}

	if(length==1){
		return vArr1[0];
	}
	
	if(length==2){
		return (vArr1[0]+vArr1[1])/2;
	}

	vArr2=__vnew(length, NULL);	

	__vsort(vArr1, length, 0, vArr2);

	if(length&1){ // odd
		start=length/2;
		len=1;
	}
	else{
		start=length/2-1;
		len=2;
	}

	value=__vmean(vArr2+start, len);

	free(vArr2);
	return value;
}

float __vvar(float *vArr1,int length,int type){
	float mValue=0;
	float value=0;

	mValue=__vmean(vArr1, length);
	for(int i=0;i<length;i++){
		value+=(vArr1[i]-mValue)*(vArr1[i]-mValue);
	}

	value=value/(!type?length-1:length);
	return value;
}

float __vstd(float *vArr1,int length,int type){
	float value=0;

	value=__vvar(vArr1,length,type);
	value=sqrtf(value);
	return value;
}

float __vcov(float *vArr1,float *vArr2,int length,int type){
	float m1=0;
	float m2=0;

	float value=0;

	m1=__vmean(vArr1, length);
	m2=__vmean(vArr2, length);
	for(int i=0;i<length;i++){
		value+=(vArr1[i]-m1)*(vArr2[i]-m2);
	}

	value=value/(!type?length-1:length);
	return value;
}

float __vcorrcoef(float *vArr1,float *vArr2,int length){
	float c1=0;
	float s1=0;
	float s2=0;

	float value=0;

	c1=__vcov(vArr1, vArr2, length, 0);
	s1=__vstd(vArr1, length, 0);
	s2=__vstd(vArr2, length, 0);

	value=c1/(s1*s2);
	return value;
}

float __vrms(float *vArr1,int length){
	float value=0;

	for(int i=0;i<length;i++){
		value+=vArr1[i]*vArr1[i];
	}

	value/=length;
	value=sqrtf(value);

	return value;
}

float __venergy(float *vArr1,int length){
	float value=0;

	for(int i=0;i<length;i++){
		value+=vArr1[i]*vArr1[i];
	}

	return value;
}

float __vzcr(float *vArr1,int length){
	float rate=0;
	int num=0;

	if(vArr1&&length){
		for(int i=1;i<length;i++){
			if(vArr1[i]*vArr1[i-1]<0){
				num++;
			}
		}

		rate=1.0*num/length;
	}
	
	return rate;
}

void __vunwrap(float *vArr1,int length,float *vArr2){
	float sub=0;

	float mod=0;
	int t=0;

	float *arr=NULL;

	if(vArr1&&length){
		if(vArr2){
			arr=vArr2;
		}
		else{
			arr=vArr1;
		}

		arr[0]=vArr1[0];
		for(int i=1;i<length;i++){
			sub=fabsf(vArr1[i]-arr[i-1]);
			if(sub<M_PI){
				arr[i]=vArr1[i];
			}
			else{
				t=floorf(sub/(2*M_PI));
				mod=sub-t*2*M_PI;
				if(mod>M_PI){
					t++;
				}

				if(vArr1[i]>vArr1[i-1]){
					arr[i]=vArr1[i]-t*2*M_PI;
				}
				else{
					arr[i]=vArr1[i]+t*2*M_PI;
				}
			}
		}
	}
}

static void __vunwrap1(float **vArr1,int length){
	float sub=0;

	float mod=0;
	int t=0;

	if(vArr1&&length){
		for(int i=1;i<length;i++){
			sub=fabsf(vArr1[i][0]-vArr1[i-1][0]);
			if(sub>=M_PI){
				t=floorf(sub/(2*M_PI));
				mod=sub-t*2*M_PI;
				if(mod>M_PI){
					t++;
				}

				if(vArr1[i][0]>vArr1[i-1][0]){
					vArr1[i][0]=vArr1[i][0]-t*2*M_PI;
				}
				else{
					vArr1[i][0]=vArr1[i][0]+t*2*M_PI;
				}
			}
		}
	}
}

// type 0 升 1降
void __vsort(float *vArr1,int length,int type,float *vArr2){
	float *arr=NULL;

	if(vArr2&&vArr2!=vArr1){
		arr=vArr2;
		memcpy(arr, vArr1, sizeof(float )*length);
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		for(int j=i+1;j<length;j++){
			float _value=0;

			if(!type){ // 升
				if(arr[i]>arr[j]){
					_value=arr[i];
					arr[i]=arr[j];
					arr[j]=_value;
				}
			}
			else{ // 降
				if(arr[i]<arr[j]){
					_value=arr[i];
					arr[i]=arr[j];
					arr[j]=_value;
				}
			}
		}
	}
}

void __vcorrsort(float *arr1,float *arr2,float *arr3,int length,int type){
	float value1=0;
	float value2=0;
	float value3=0;

	for(int i=0;i<length;i++){
		for(int j=i+1;j<length;j++){
			if(!type){ // asc
				if(arr1[i]>arr1[j]){
					value1=arr1[i];
					arr1[i]=arr1[j];
					arr1[j]=value1;

					if(arr2){
						value2=arr2[i];
						arr2[i]=arr2[j];
						arr2[j]=value2;
					}
					
					if(arr3){
						value3=arr3[i];
						arr3[i]=arr3[j];
						arr3[j]=value3;
					}
				}
			}
			else{ // desc
				if(arr1[i]<arr1[j]){
					value1=arr1[i];
					arr1[i]=arr1[j];
					arr1[j]=value1;

					if(arr2){
						value2=arr2[i];
						arr2[i]=arr2[j];
						arr2[j]=value2;
					}
					
					if(arr3){
						value3=arr3[i];
						arr3[i]=arr3[j];
						arr3[j]=value3;
					}
				}
			}
		}
	}
}

void __vcorrsort1(float *arr1,float *arr2,float *arr3,int *arr4,int length,int type){
	float value1=0;
	float value2=0;
	float value3=0;
	
	int value4=0;

	for(int i=0;i<length;i++){
		for(int j=i+1;j<length;j++){
			if(!type){ // asc
				if(arr1[i]>arr1[j]){
					value1=arr1[i];
					arr1[i]=arr1[j];
					arr1[j]=value1;

					if(arr2){
						value2=arr2[i];
						arr2[i]=arr2[j];
						arr2[j]=value2;
					}
					
					if(arr3){
						value3=arr3[i];
						arr3[i]=arr3[j];
						arr3[j]=value3;
					}

					if(arr4){
						value4=arr4[i];
						arr4[i]=arr4[j];
						arr4[j]=value4;
					}
				}
			}
			else{ // desc
				if(arr1[i]<arr1[j]){
					value1=arr1[i];
					arr1[i]=arr1[j];
					arr1[j]=value1;

					if(arr2){
						value2=arr2[i];
						arr2[i]=arr2[j];
						arr2[j]=value2;
					}
					
					if(arr3){
						value3=arr3[i];
						arr3[i]=arr3[j];
						arr3[j]=value3;
					}

					if(arr4){
						value4=arr4[i];
						arr4[i]=arr4[j];
						arr4[j]=value4;
					}
				}
			}
		}
	}
}

void __vsorti(int *vArr1,int length,int type,int *vArr2){
	int *arr=NULL;

	if(vArr2&&vArr2!=vArr1){
		arr=vArr2;
		memcpy(arr, vArr1, sizeof(int )*length);
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		for(int j=i+1;j<length;j++){
			int _value=0;

			if(!type){ // asc
				if(arr[i]>arr[j]){
					_value=arr[i];
					arr[i]=arr[j];
					arr[j]=_value;
				}
			}
			else{ // desc
				if(arr[i]<arr[j]){
					_value=arr[i];
					arr[i]=arr[j];
					arr[j]=_value;
				}
			}
		}
	}
}

int __vindex(float *vArr1,int length,float value){
	int index=-1;

	for(int i=0;i<length;i++){
		if(fabsf(vArr1[i]-value)<1e-6){
			index=i;
			break;
		}
	}

	return index;
}

int __vindexi(int *vArr1,int length,int value){
	int index=-1;

	for(int i=0;i<length;i++){
		if(vArr1[i]==value){
			index=i;
			break;
		}
	}

	return index;
}

int __vhas(float *vArr1,int length,float value){
	int flag=0;

	for(int i=0;i<length;i++){
		if(fabsf(vArr1[i]-value)<1e-6){
			flag=1;
			break;
		}
	}

	return flag;
}

int __vhasi(int *vArr1,int length,int value){
	int flag=0;

	for(int i=0;i<length;i++){
		if(vArr1[i]==value){
			flag=1;
			break;
		}
	}

	return flag;
}

// element math相关
void __vmap(float *vArr1,int length,void *callback,float *vArr2){
	float *arr=NULL;
	UniFunc call=NULL;

	call=(UniFunc )callback;
	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=call(vArr1[i]);
	}
}

void __vmap1(float *vArr1,int length,void *callback1,float value,float *vArr2){
	float *arr=NULL;
	UniFunc1 call=NULL;

	call=(UniFunc1 )callback1;
	if(vArr2){
		arr=vArr2;
	}
	else{
		arr=vArr1;
	}

	for(int i=0;i<length;i++){
		arr[i]=call(vArr1[i],value);
	}
}

// index/range/liespace/transpose/new相关
float *__vnew(int length,float *value){
	float *arr=NULL;
	float _value=0;

	arr=(float *)calloc(length, sizeof(float ));
	if(value){
		_value=*value;
	}

	if(_value!=0){
		for(int i=0;i<length;i++){
			arr[i]=_value;
		}
	}
	
	return arr;
}

// type 0 has stop 1 no stop
float *__vlinspace(float start,float stop,int length,int type){
	float *arr=NULL;
	float step=0;

	arr=__vnew(length,NULL);
	if(type==0){
		step=(stop-start)/(length-1>0?length-1:1);
	}
	else{
		step=(stop-start)/length;
	}
	
	for(int i=0;i<length;i++){
		arr[i]=start+i*step;
	}

	return arr;
}

float *__vlogspace(float start,float stop,int length,int type){
	float *arr=NULL;

	arr=__vlinspace(start,stop,length,type);
	for(int i=0;i<length;i++){
		arr[i]=powf(10, arr[i]);
	}

	return arr;
}

int __varange(float start,float stop,float step,float **outArr){
	float *arr=NULL;
	int length=0;

	if(stop<=start||!outArr){
		return 0;
	}

	length=ceilf((stop-start)/step);
	arr=__vnew(length, NULL);
	for(int i=0;i<length;i++){
		arr[i]=start+i*step;
	}

	*outArr=arr;
	return length;
}

void __vfill(float *arr,int length,float value){

	for(int i=0;i<length;i++){
		arr[i]=value;
	}
}

void __vcopy(float *dstArr,float *srcArr,int length){

	memcpy(dstArr, srcArr, sizeof(float )*length);
}

void __mtrans(float *mArr1,int nLength,int mLength,float *mArr3){
	int index=0;

	if(!mArr3||mArr3==mArr1){
		return;
	}

	for(int i=0;i<mLength;i++){
		for(int j=0;j<nLength;j++){
			mArr3[index]=mArr1[i+j*mLength];
			index++;
		}
	}
}

float *__vget(float *vArr1,int length,VSlice *slice){
	float *vArr2=NULL;

	int nLen=0;

	int *rIndexArr=NULL;

	int rIndex=0;
	int index=0;

	if(!slice){
		return NULL;
	}
	
	if(slice->nLength>0){
		rIndexArr=slice->indexArr;
		nLen=slice->nLength;
	}
	else{
		nLen=length;
	}

	vArr2=__vnew(nLen, NULL);
	for(int i=0;i<nLen;i++){
		if(slice->nLength>0){
			rIndex=rIndexArr[i];
		}
		else{
			if(slice->nLength==0){  
				rIndex=i;
			}
			else{ // -1
				rIndex=nLen-1-i;
			}
		}

		vArr2[index]=vArr1[rIndex];
		index++;
	}

	return vArr2;
}

void __vset(float *vArr1,int length,VSlice *slice,float *vArr2){
	int nLen=0;

	int *rIndexArr=NULL;

	int rIndex=0;
	int index=0;

	if(!slice){
		return ;
	}
	
	if(slice->nLength>0){
		rIndexArr=slice->indexArr;
		nLen=slice->nLength;
	}
	else{
		nLen=length;
	}

	for(int i=0;i<nLen;i++){
		if(slice->nLength>0){
			rIndex=rIndexArr[i];
		}
		else{
			if(slice->nLength==0){  
				rIndex=i;
			}
			else{ // -1
				rIndex=nLen-1-i;
			}
		}

		vArr1[rIndex]=vArr2[index];
		index++;
	}
}

/***
	[:,:]
	nLength => i row
	mLength => j col
	0 => range(0,nLength/mLength)
	-1 => range(nLength/mLength,0)
****/
float *__mget(float *mArr1,int nLength,int mLength,VSlice *slice){
	float *mArr2=NULL;

	int nLen=0;
	int mLen=0;

	int *rIndexArr=NULL;
	int *cIndexArr=NULL;

	int rIndex=0;
	int cIndex=0;

	int index=0;

	if(!slice){
		return NULL;
	}
	
	if(slice->nLength>0){
		rIndexArr=slice->indexArr;
		nLen=slice->nLength;
	}
	else{
		nLen=nLength;
	}

	if(slice->mLength>0){
		if(slice->nLength>0){
			cIndexArr=slice->indexArr+slice->nLength;
		}
		else{
			cIndexArr=slice->indexArr;
		}
		mLen=slice->mLength;
	}
	else{
		mLen=mLength;
	}

	mArr2=__vnew(nLen*mLen, NULL);
	for(int i=0;i<nLen;i++){
		if(slice->nLength>0){
			rIndex=rIndexArr[i];
		}
		else{
			if(slice->nLength==0){  
				rIndex=i;
			}
			else{ // -1
				rIndex=nLen-1-i;
			}
		}

		for(int j=0;j<mLen;j++){
			if(slice->mLength>0){
				cIndex=cIndexArr[j];
			}
			else{
				if(slice->mLength==0){  
					cIndex=j;
				}
				else{ // -1
					cIndex=mLen-1-j;
				}
			}

			mArr2[index]=mArr1[rIndex*mLength+cIndex];
			index++;
		}
	}

	return mArr2;
}

void __mset(float *mArr1,int nLength,int mLength,VSlice *slice,float *mArr2){
	int nLen=0;
	int mLen=0;

	int *rIndexArr=NULL;
	int *cIndexArr=NULL;

	int rIndex=0;
	int cIndex=0;

	int index=0;

	if(!slice){
		return ;
	}
	
	if(slice->nLength>0){
		rIndexArr=slice->indexArr;
		nLen=slice->nLength;
	}
	else{
		nLen=nLength;
	}

	if(slice->mLength>0){
		if(slice->nLength>0){
			cIndexArr=slice->indexArr+slice->nLength;
		}
		else{
			cIndexArr=slice->indexArr;
		}
		mLen=slice->mLength;
	}
	else{
		mLen=mLength;
	}

	for(int i=0;i<nLen;i++){
		if(slice->nLength>0){
			rIndex=rIndexArr[i];
		}
		else{
			if(slice->nLength==0){  
				rIndex=i;
			}
			else{ // -1
				rIndex=nLen-1-i;
			}
		}

		for(int j=0;j<mLen;j++){
			if(slice->mLength>0){
				cIndex=cIndexArr[j];
			}
			else{
				if(slice->mLength==0){  
					cIndex=j;
				}
				else{ // -1
					cIndex=mLen-1-j;
				}
			}

			mArr1[rIndex*mLength+cIndex]=mArr2[index];
			index++;
		}
	}
}

void __mset_value(float *mArr1,int nLength,int mLength,VSlice *slice,float value){
	int nLen=0;
	int mLen=0;

	int *rIndexArr=NULL;
	int *cIndexArr=NULL;

	int rIndex=0;
	int cIndex=0;

	if(!slice){
		return ;
	}
	
	if(slice->nLength>0){
		rIndexArr=slice->indexArr;
		nLen=slice->nLength;
	}
	else{
		nLen=nLength;
	}

	if(slice->mLength>0){
		if(slice->nLength>0){
			cIndexArr=slice->indexArr+slice->nLength;
		}
		else{
			cIndexArr=slice->indexArr;
		}
		mLen=slice->mLength;
	}
	else{
		mLen=mLength;
	}

	for(int i=0;i<nLen;i++){
		if(slice->nLength>0){
			rIndex=rIndexArr[i];
		}
		else{
			if(slice->nLength==0){  
				rIndex=i;
			}
			else{ // -1
				rIndex=nLen-1-i;
			}
		}

		for(int j=0;j<mLen;j++){
			if(slice->mLength>0){
				cIndex=cIndexArr[j];
			}
			else{
				if(slice->mLength==0){  
					cIndex=j;
				}
				else{ // -1
					cIndex=mLen-1-j;
				}
			}

			mArr1[rIndex*mLength+cIndex]=value;
		}
	}
}

void __mset_vector(float *mArr1,int nLength,int mLength,VSlice *slice,int axis,float *vArr1){
	int nLen=0;
	int mLen=0;

	int nLength1=0;
	int mLength1=0;

	int *rIndexArr=NULL;
	int *cIndexArr=NULL;

	int rIndex=0;
	int cIndex=0;

	if(!slice){
		return ;
	}
	
	if(slice->nLength>0){
		rIndexArr=slice->indexArr;
		nLength1=slice->nLength;
	}
	else{
		nLength1=nLength;
	}

	if(slice->mLength>0){
		if(slice->nLength>0){
			cIndexArr=slice->indexArr+slice->nLength;
		}
		else{
			cIndexArr=slice->indexArr;
		}
		mLength1=slice->mLength;
	}
	else{
		mLength1=mLength;
	}

	if(axis==0){
		nLen=mLength1;
		mLen=nLength1;
	}
	else{
		nLen=nLength1;
		mLen=mLength1;
	}

	for(int i=0;i<nLen;i++){
		if(axis==0){ // ==mLength1
			if(slice->mLength>0){
				rIndex=cIndexArr[i];
			}
			else{
				if(slice->mLength==0){  
					rIndex=i;
				}
				else{ // -1
					rIndex=mLength1-1-i;
				}
			}
		}
		else{ // ==nLength1
			if(slice->nLength>0){
				rIndex=rIndexArr[i];
			}
			else{
				if(slice->nLength==0){  
					rIndex=i;
				}
				else{ // -1
					rIndex=nLength1-1-i;
				}
			}
		}

		for(int j=0;j<mLen;j++){
			if(axis==0){ // ==nLength1
				if(slice->nLength>0){
					cIndex=rIndexArr[j];
				}
				else{
					if(slice->nLength==0){  
						cIndex=j;
					}
					else{ // -1
						cIndex=nLength1-1-j;
					}
				}
			}
			else{ // ==mLength1
				if(slice->mLength>0){
					cIndex=cIndexArr[j];
				}
				else{
					if(slice->mLength==0){  
						cIndex=j;
					}
					else{ // -1
						cIndex=mLength1-1-j;
					}
				}
			}

			if(axis==0){
				mArr1[rIndex+cIndex*mLength]=vArr1[i];
			}
			else{
				mArr1[rIndex*mLength+cIndex]=vArr1[i];
			}
		}
	}
}

// astype
void __vf2i(float *vArr1,int length,int *vArr2){
	
	if(!vArr1||!vArr2){
		return;
	}

	for(int i=0;i<length;i++){
		vArr2[i]=floorf(vArr1[i]);
	}
}

void __vi2f(int *vArr1,int length,float *vArr2){
	
	if(!vArr1||!vArr2){
		return;
	}

	for(int i=0;i<length;i++){
		vArr2[i]=vArr1[i];
	}
}

// repeat axis 0 1*m 1 n*1
void __vrepeat(float *vArr1,int length,int num,float *vArr3){

	// if(axis==0){ // 1*m => num*length
	// 	for(int i=0;i<num;i++){
	// 		for(int j=0;j<length;j++){
	// 			mArr3[i*length+j]=vArr1[j];
	// 		}
	// 	}
	// }
	// else{ // n*1 => length*num
	// 	for(int i=0;i<num;i++){
	// 		for(int j=0;j<length;j++){
	// 			mArr3[i+j*num]=vArr1[j];
	// 		}
	// 	}
	// }

	for(int i=0;i<num;i++){
		for(int j=0;j<length;j++){
			vArr3[i*length+j]=vArr1[j];
		}
	}
}

void __mrepeat(float *mArr1,int nLength,int mLength,int axis,int num,float *mArr3){
	int length=0;

	if(axis==0){ // n*m => (n*num)*m
		length=nLength*num;
		for(int i=0;i<length;i++){
			for(int j=0;j<mLength;j++){
				mArr3[i*mLength+j]=mArr1[i*mLength%(nLength*mLength)+j];
			}
		}
	}
	else{ // n*m => n*(m*num)
		length=mLength*num;
		for(int i=0;i<length;i++){
			for(int j=0;j<nLength;j++){
				mArr3[i+j*length]=mArr1[i%mLength+j*mLength];
			}
		}
	}
}

void __vconcat(float *vArr1,float *vArr2,int length1,int length2,float *vArr3){

	for(int i=0;i<length1;i++){
		vArr3[i]=vArr1[i];
	}

	for(int i=0;i<length2;i++){
		vArr3[i+length1]=vArr2[i];
	}
}

void __mconcat(float *mArr1,float *mArr2,
				int nLength1,int mLength1,
				int nLength2,int mLength2,
				int axis,
				float *mArr3){
	if(axis==0){ // n1*m1 n2*m2 m1==m2
		if(mLength1!=mLength2){
			return;
		}

		for(int i=0;i<nLength1;i++){
			for(int j=0;j<mLength1;j++){
				mArr3[i*mLength1+j]=mArr1[i*mLength1+j];
			}
		}

		for(int i=0;i<nLength2;i++){
			for(int j=0;j<mLength2;j++){
				mArr3[(i+nLength1)*mLength2+j]=mArr2[i*mLength2+j];
			}
		}
	}
	else{ // n1*m1 n2*m2 n1==n2
		if(nLength1!=nLength2){
			return;
		}
		
		for(int i=0;i<mLength1;i++){
			for(int j=0;j<nLength1;j++){
				mArr3[i+j*(mLength1+mLength2)]=mArr1[i+j*mLength1];
			}
		}

		for(int i=0;i<mLength2;i++){
			for(int j=0;j<nLength2;j++){
				mArr3[i+mLength1+j*(mLength1+mLength2)]=mArr2[i+j*mLength2];
			}
		}	
	}
}

void __mcut(float *mArr1,int nLength,int mLength,
			int nIndex,int nLength1,
			int mIndex,int mLength1,
			float *mArr3){
	float *arr=NULL;
	int index=0;

	if(nIndex<=0||
		nIndex>nLength-1||
		mIndex<=0||
		mIndex>mLength-1||
		nIndex+nLength1>nLength||
		mIndex+mLength1>mLength){
		return;
	}

	if(mArr3){
		arr=mArr3;
	}
	else{
		arr=mArr1;
	}

	for(int i=nIndex;i<nLength1+nIndex;i++){
		for(int j=mIndex;j<mLength1+mIndex;j++){
			arr[index]=mArr1[i*mLength+j];
			index++;
		}
	}
}

// debug vector/matrix相关
void __vdebug(float *vArr1,int length,int type){
	if(type){
		printf("vector is:\n");

		printf("	");
		for(int i=0;i<length;i++){
			printf("%d:%f ,",i,vArr1[i]);
		}
	}
	else{
		printf("vector([");
		for(int i=0;i<length-1;i++){
			printf("%f, ",vArr1[i]);
		}
		printf("%f",vArr1[length-1]);
		printf("])\n");
	}
}

void __mdebug(float *mArr1,int nLength,int mLength,int type){
	if(type){
		printf("matrix is:\n");

		for(int i=0;i<nLength;i++){
			printf("	%d:\n",i);
			printf("		");
			for(int j=0;j<mLength;j++){
				printf("%d:%f ,",j,mArr1[i*mLength+j]);
			}

			printf("\n\n");
		}
	}
	else{
		printf("matrix([");
		for(int i=0;i<nLength-1;i++){
			printf("[");

			for(int j=0;j<mLength-1;j++){
				printf("%f ,",mArr1[i*mLength+j]);
			}
			printf("%f",mArr1[i*mLength+mLength-1]);

			printf("],");
			printf("\n        ");
		}

		printf("[");
		for(int j=0;j<mLength-1;j++){
			printf("%f ,",mArr1[(nLength-1)*mLength+j]);
		}
		printf("%f",mArr1[(nLength-1)*mLength+mLength-1]);

		printf("]");
		printf("])\n");
	}
}

void __mdiff(float *mArr1,int nLength,int mLength,int axis,int *order,float *mArr3){
	int nLen=0;
	int mLen=0;

	int _order=1;

	if(!mArr3){
		return;
	}

	if(order){
		_order=*order;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	for(int i=0;i<nLength*mLength;i++){
		mArr3[i]=mArr1[i];
	}

	while(_order>0&&mLen>1){
		for(int i=0;i<nLen;i++){
			for(int j=1;j<mLen;j++){
				if(axis==0){ // 1*m
					mArr3[i+(j-1)*mLength]=mArr3[i+j*mLength]-mArr3[i+(j-1)*mLength];
				}
				else{ // n*1
					mArr3[i*mLength+j-1]=mArr3[i*mLength+j]-mArr3[i*mLength+j-1];
					mLength--;
				}
			}
		}

		_order--;
		mLen--;
	}
}

// step 1
void __mdiff2(float *mArr1,int nLength,int mLength,int axis,int *step,float *mArr3){
	int nLen=0;
	int mLen=0;

	int _step=1;

	if(!mArr3){
		return;
	}

	if(step){
		_step=*step;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	for(int i=0;i<nLength*mLength;i++){
		mArr3[i]=mArr1[i];
	}

	if(_step>0){
		for(int i=0;i<nLen;i++){
			for(int j=0;j<mLen;j++){
				if(axis==0){ // 1*m
					if(j<_step){
						mArr3[i+j*mLength]=0;
					}
					else{
						mArr3[i+j*mLength]=mArr3[i+j*mLength]-mArr1[i+(j-_step)*mLength];
					}
				}
				else{ // n*1
					if(j<_step){
						mArr3[i*mLength+j]=0;
					}
					else{
						mArr3[i*mLength+j]=mArr3[i*mLength+j]-mArr1[i*mLength+j-_step];
					}
				}
			}
		}
	}
}

void __mdiff3(float *mArr1,float *mArr2,int nLength,int mLength,int axis,int *step,float *mArr3){


}

// type 0 max 1 median
static void __mxfilter(float *mArr1,int nLength,int mLength,int type,int axis,int order,float *mArr3){
	int nLen=0;
	int mLen=0;

	float *vArr1=NULL;
	float *vArr2=NULL;

	if(!mArr3||order<1){
		return;
	}

	if(axis==0){
		nLen=mLength;
		mLen=nLength;
	}
	else{
		nLen=nLength;
		mLen=mLength;
	}

	vArr1=__vnew(mLen, NULL);
	vArr2=__vnew(mLen, NULL);

	for(int i=0;i<nLen;i++){
		if(axis==0){ // 1*m
			for(int j=0;j<mLen;j++){
				vArr1[j]=mArr1[i+j*mLength];
			}

			if(type==0){
				__vmaxfilter(vArr1,mLen,order,vArr2);
			}
			else{
				__vmedianfilter(vArr1,mLen,order,vArr2);
			}

			for(int j=0;j<mLen;j++){
				mArr3[i+j*mLength]=vArr2[j];
			}
		}
		else{
			if(type==0){
				__vmaxfilter(mArr1+i*mLength,mLen,order,vArr2);
			}
			else{
				__vmedianfilter(mArr1+i*mLength,mLen,order,vArr2);
			}

			for(int j=0;j<mLen;j++){
				mArr3[i*mLength+j]=vArr2[j];
			}
		}
	}

	free(vArr1);
	free(vArr2);
}

void __mmaxfilter(float *mArr1,int nLength,int mLength,int axis,int order,float *mArr3){
	
	__mxfilter(mArr1,nLength,mLength,0,axis,order,mArr3);
}

void __mmedianfilter(float *mArr1,int nLength,int mLength,int axis,int order,float *mArr3){
	
	if(order>1&&(order&1)){
		__mxfilter(mArr1,nLength,mLength,1,axis,order,mArr3);
	}
}

void __vdiff(float *vArr1,int length,int *order,float *vArr3){
	int _order=1;

	if(!vArr3){
		return;
	}

	if(order){
		_order=*order;
	}

	for(int i=0;i<length;i++){
		vArr3[i]=vArr1[i];
	}

	while(_order>0&&length>1){
		for(int i=1;i<length;i++){
			vArr3[i-1]=vArr3[i]-vArr3[i-1];
		}

		_order--;
		length--;
	}
}

// step 1
void __vdiff2(float *vArr1,int length,int *step,float *vArr3){
	int _step=1;

	if(!vArr3){
		return;
	}

	if(step){
		_step=*step;
	}

	if(_step>0){
		memset(vArr3, 0, sizeof(float )*_step);
		for(int i=_step;i<length;i++){
			vArr3[i]=vArr1[i];
		}

		for(int i=_step;i<length;i++){
			vArr3[i]=vArr3[i]-vArr1[i-_step];
		}
	}
}

void __vmaxfilter(float *vArr1,int length,int order,float *vArr3){
	int left=0;
	int right=0;

	int start=0;
	int end=0;

	if(order<1||!vArr3){
		return;
	}

	left=order/2;
	right=order-left;
	for(int i=0;i<length;i++){
		start=(i-left>=0?i-left:0);
		end=(i-1+right<=length-1?i-1+right:length-1);
		vArr3[i]=__arr_max(vArr1+start, end-start+1);
	}
}

void __vmedianfilter(float *vArr1,int length,int order,float *vArr3){
	float *arr1=NULL;

	int len=0;

	if((order&1)==0||order<2||!vArr3){
		return;
	}

	len=order/2;
	arr1=__vnew(length+2*len, NULL);
	memcpy(arr1+len, vArr1, sizeof(float )*length);

	for(int i=len,j=0;i<length+len;i++,j++){
		float value=0;

		value=__vmedian(arr1+(i-len), order);
		vArr3[j]=value;
	}

	free(arr1);
}

static float __arr_max(float *vArr,int length){
	float max=0;

	if(!vArr||!length){
		return 0;
	}

	max=vArr[0];
	for(int i=1;i<length;i++){
		if(max<vArr[i]){
			max=vArr[i];
		}
	}

	return max;
}





```

---

### Archivo: `./src/vector/flux_vectorOp.h`

```


#ifndef FLUX_VECTOROP_H
#define FLUX_VECTOROP_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

// element math相关
// abs/ng/floor/ceil/round vector==matrix
void __vabs(float *vArr1,int length,float *vArr2);
void __vng(float *vArr1,int length,float *vArr2);
void __vfloor(float *vArr1,int length,float *vArr2);
void __vceil(float *vArr1,int length,float *vArr2);
void __vround(float *vArr1,int length,float *vArr2);

// cos/sin/tan/acos/asin/atan
void __vcos(float *vArr1,int length,float *vArr2);
void __vsin(float *vArr1,int length,float *vArr2);
void __vtan(float *vArr1,int length,float *vArr2);
void __vacos(float *vArr1,int length,float *vArr2);
void __vasin(float *vArr1,int length,float *vArr2);
void __vatan(float *vArr1,int length,float *vArr2);

// exp/exp2/pow/sqrt
void __vexp(float *vArr1,int length,float *vArr2);
void __vexp2(float *vArr1,int length,float *vArr2);
void __vpow(float *vArr1,float exp,int length,float *vArr2);
void __vsqrt(float *vArr1,int length,float *vArr2);

// log/log10/log2
void __vlog(float *vArr1,int length,float *vArr2);
void __vlog10(float *vArr1,int length,float *vArr2);
void __vlog2(float *vArr1,int length,float *vArr2);

// log compress
void __vlog_compress(float *vArr1,float *gamma,float *base,int length,float *vArr2);
void __vlog10_compress(float *vArr1,float *gamma,float *base,int length,float *vArr2);
void __vlog2_compress(float *vArr1,float *gamma,float *base,int length,float *vArr2);

// sinc
void __vsinc(float *vArr1,int length,float *vArr2);
void __vsinc_low(float *vArr1,int length,float cut,float *vArr2);
void __vsinc_high(float *vArr1,int length,float cut,float *vArr2);
void __vsinc_bandpass(float *vArr1,int length,float cut1,float cut2,float *vArr2);
void __vsinc_stop(float *vArr1,int length,float cut1,float cut2,float *vArr2);

// gradient edge 1/2
void __vgradient(float *vArr1,int length,int edgeOrder,float *vArr2);

// interpolation
void __vinterp_linear(float *xArr1,float *yArr1,int length1,float *xArr2,int length2,float *yArr2);

// pad type 0 'constant' 1 'refect' 2 'wrap' 3 'symmetric' 4 'edge'
void __vpad(float *vArr1,int length,
			int headLen,int tailLen,int type,
			float *value1,float *value2,
			float *vArr2);

void __mpad(float *mArr1,int nlength,int mLength,
			int headLen,int tailLen,int type,
			float *value1,float *value2,
			int axis,
			float *mArr2);

// constant
void __vpad_center1(float *vArr1,int vLength,
				int leftLength,int rightLength,
				float value1,float value2);
void __vpad_left1(float *vArr1,int vLength,int leftLength,int value);
void __vpad_right1(float *vArr1,int vLength,int rightLength,int value);

// reflect
void __vpad_center2(float *vArr1,int vLength,int leftLength,int rightLength);
void __vpad_left2(float *vArr1,int vLength,int leftLength);
void __vpad_right2(float *vArr1,int vLength,int rightLength);

// wrap
void __vpad_center3(float *vArr1,int vLength,int leftLength,int rightLength);
void __vpad_left3(float *vArr1,int vLength,int leftLength);
void __vpad_right3(float *vArr1,int vLength,int rightLength);

// symmetric
void __vpad_center4(float *vArr1,int vLength,int leftLength,int rightLength);
void __vpad_left4(float *vArr1,int vLength,int leftLength);
void __vpad_right4(float *vArr1,int vLength,int rightLength);

// edge
void __vpad_center5(float *vArr1,int vLength,int leftLength,int rightLength);
void __vpad_left5(float *vArr1,int vLength,int leftLength);
void __vpad_right5(float *vArr1,int vLength,int rightLength);



#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/flux_temporal.c`

```
// 

#include <string.h>
#include <math.h>

#include "flux_temporal.h"




```

---

### Archivo: `./src/bft_algorithm.c`

```
// 

#include <string.h>
#include <math.h>

#include "vector/flux_vector.h"
#include "vector/flux_vectorOp.h"
#include "vector/flux_complex.h"

#include "util/flux_util.h"

#include "dsp/flux_correct.h"

#include "filterbank/auditory_filterBank.h"

#include "temporal_algorithm.h"
#include "reassign_algorithm.h"

#include "bft_algorithm.h"

struct OpaqueBFT{
	ReassignObj reassignObj;

	int fftLength; // fftLength,timeLength,num
	int timeLength;

	int num;
	float *mFilterBankArr; // num*(fftLength/2+1)
	float *mArr1; // image cache 

	float *freBandArr;
	int *binBandArr;

	TemporalObj tempObj;

	// rea
	float *mRealArr; // rea r,i(timeLength*(fftLength/2+1)) -> power r(timeLength*(fftLength/2+1)) 
	float *mImageArr;

	// params
	int samplate; // filterBank 
	float lowFre;
	float highFre;

	int lowIndex; // only for linear
	int highIndex;

	int binPerOctave; // log

	int radix2Exp; // rea
	WindowType windowType;
	int slideLength;

	SpectralDataType dataType; // data&&filterBank
	SpectralFilterBankScaleType filterScaleType;
	SpectralFilterBankStyleType filterStyleType;
	SpectralFilterBankNormalType filterNormalType;

	int resultType; // 0 complex 1 real->mRealArr
	float normValue;  // default 1; >0 mag=>result power=>S

	int isReassign; 
	int isTemporal; 

};

static void __bftObj_init(BFTObj bftObj);

/***
	num>=2&&num<=2048
	samplate 32000
	lowFre linear 0 mel/bark/erb/log 27.5
	highFre 16000
	binPerOctave 12 >=4&&<=48
	
	radix2Exp 12 
	WindowType "hann"
	slideLength 1024

	filterScaleType "linear"
	filterStyleType "slaney"
	filterNormalType "none"
	dataType "power"

	isReassign 0
****/
int bftObj_new(BFTObj *bftObj,int num,int radix2Exp,
			int *samplate,float *lowFre,float *highFre,int *binPerOctave,
			WindowType *windowType,int *slideLength,
			SpectralFilterBankScaleType *filterScaleType,
			SpectralFilterBankStyleType *filterStyleType,
			SpectralFilterBankNormalType *filterNormalType,
			SpectralDataType *dataType,
			int *isReassign,
			int *isTemporal){
	int status=0;
	BFTObj bft=NULL;

	int fftLength=0;

	int _samplate=32000; // filterBank 
	float _lowFre=0;
	float _highFre=0;

	int lowIndex=0; // only for linear
	int highIndex=0;

	int _binPerOctave=12; // log
	int _radix2Exp=12; // reassign

	WindowType _windowType=Window_Hann;
	int _slideLength=0;

	SpectralDataType _dataType=SpectralData_Power; // data&&filterBank
	SpectralFilterBankScaleType _filterScaleType=SpectralFilterBankScale_Linear;
	SpectralFilterBankStyleType _filterStyleType=SpectralFilterBankStyle_Slaney;
	SpectralFilterBankNormalType _filterNormalType=SpectralFilterBankNormal_None;

	int _isReassign=0;
	int _isTemporal=0;

	if(radix2Exp){
		_radix2Exp=radix2Exp;
		if(_radix2Exp<1||_radix2Exp>30){
			status=-100;
			printf("radix2Exp is error!\n");
			return status;
		}
	}

	fftLength=1<<_radix2Exp;
	if(samplate){
		if(*samplate>0&&*samplate<=196000){
			_samplate=*samplate;
		}
	}

	if(dataType){
		_dataType=*dataType;
	}
	
	if(filterScaleType){
		_filterScaleType=*filterScaleType;
		if(_filterScaleType>SpectralFilterBankScale_Log){
			printf("scaleType is error!\n");
			return 1;
		}
	}

	if(filterStyleType){
		_filterStyleType=*filterStyleType;
	}
	
	if(filterNormalType){
		_filterNormalType=*filterNormalType;
	}

	_highFre=_samplate/2.0;

	if(lowFre){
		if(*lowFre>=0&&*lowFre<_samplate/2.0){
			_lowFre=*lowFre;
		}
	}

	if(_lowFre==0){
		if(_filterScaleType==SpectralFilterBankScale_Octave||
			_filterScaleType==SpectralFilterBankScale_Log){ // Log/Logspace

			_lowFre=powf(2, -45/12.0)*440;
			_highFre=powf(2, 38/12.0)*440;
		}
	}

	if(highFre){
		if(*highFre>0&&*highFre<=_samplate/2.0){
			_highFre=*highFre;
		}
	}

	if(_highFre<_lowFre){
		_lowFre=0;
		_highFre=_samplate/2.0;
		if(_filterScaleType==SpectralFilterBankScale_Octave||
			_filterScaleType==SpectralFilterBankScale_Log){ // Log/Logspace

			_lowFre=powf(2, -45/12.0)*440;
			_highFre=powf(2, 38/12.0)*440;
		}
	}

	if(binPerOctave){
		if(*binPerOctave>=4&&*binPerOctave<=48){
			_binPerOctave=*binPerOctave;
		}
	}

	if(windowType){
		_windowType=*windowType;
	}

	_slideLength=fftLength/4;
	if(slideLength){
		if(*slideLength>0){ // &&*slideLength<=fftLength ->support not overlap
			_slideLength=*slideLength;
		}
	}

	if(_filterScaleType==SpectralFilterBankScale_Linear){ // linear
		float det=0;

		det=_samplate/(float )fftLength;
		auditory_reviseLinearFre(num, _lowFre,_highFre, det,1,&_lowFre, &_highFre);

		lowIndex=roundf(_lowFre/det);
		highIndex=roundf(_highFre/det);

		if(_highFre>_samplate/2.0){
			printf("scale linear: lowFre and num is large, overflow error\n");
			return -1;
		}
	}
	else if(_filterScaleType==SpectralFilterBankScale_Octave){ // log
		auditory_reviseLogFre(num, _lowFre,_highFre, _binPerOctave,1, &_lowFre, &_highFre);

		if(_highFre>_samplate/2.0){
			printf("scale log: lowFre and num is large, overflow error!\n");
			return -1;
		}
	}

	if(isReassign){
		_isReassign=*isReassign;
	}

	if(isTemporal){
		_isTemporal=*isTemporal;
	}

	if(num<2||num>fftLength/2+1){ 
		printf("num is error!\n");
		return -1;
	}

	bft=*bftObj=(BFTObj )calloc(1, sizeof(struct OpaqueBFT ));

	bft->fftLength=fftLength;
	bft->num=num;

	bft->samplate=_samplate;
	bft->lowFre=_lowFre;
	bft->highFre=_highFre;

	bft->lowIndex=lowIndex;
	bft->highIndex=highIndex;

	bft->binPerOctave=_binPerOctave;

	bft->radix2Exp=_radix2Exp;
	bft->windowType=_windowType;
	bft->slideLength=_slideLength;

	bft->dataType=_dataType;
	bft->filterScaleType=_filterScaleType;
	bft->filterStyleType=_filterStyleType;
	bft->filterNormalType=_filterNormalType;

	bft->normValue=1;

	bft->isReassign=_isReassign;
	bft->isTemporal=_isTemporal;

	__bftObj_init(bft);

	return status;
}

static void __bftObj_init(BFTObj bftObj){
	ReassignObj reassignObj=NULL;

	int num=0;
	int fftLength=0;

	float *mFilterBankArr=NULL;
	float *mArr1=NULL;

	float *freBandArr=NULL;
	int *binBandArr=NULL;

	int samplate=0; // filterBank 

	float lowFre=0;
	float highFre=0;

	int binPerOctave=0;
	int radix2Exp=0; // stft
	WindowType windowType;
	int slideLength=0;

	SpectralFilterBankScaleType filterScaleType;
	SpectralFilterBankStyleType filterStyleType;
	SpectralFilterBankNormalType filterNormalType;

	int isReassign=0;

	TemporalObj tempObj=NULL;

	ReassignType reType=Reassign_None;

	num=bftObj->num;
	fftLength=bftObj->fftLength;

	samplate=bftObj->samplate;
	lowFre=bftObj->lowFre;
	highFre=bftObj->highFre;

	int lowIndex=0; // only for linear
	int highIndex=0;

	binPerOctave=bftObj->binPerOctave;

	radix2Exp=bftObj->radix2Exp;
	windowType=bftObj->windowType;
	slideLength=bftObj->slideLength;

	filterScaleType=bftObj->filterScaleType;
	filterStyleType=bftObj->filterStyleType;
	filterNormalType=bftObj->filterNormalType;

	isReassign=bftObj->isReassign;

	if(isReassign){
		reType=Reassign_All;
	}

	// 1. reassign
	reassignObj_new(&reassignObj,radix2Exp,
					&samplate,&windowType,&slideLength,
					&reType,NULL,
					NULL,NULL);

	// 2. filterBank
	if(filterScaleType>=SpectralFilterBankScale_Linear&&
		filterScaleType<=SpectralFilterBankScale_Log){

		mFilterBankArr=__vnew(num*(fftLength/2+1), NULL);
		mArr1=__vnew(num*(fftLength/2+1), NULL);

		freBandArr=__vnew(num+2, NULL); 
		binBandArr=__vnewi(num+2, NULL);

		if(filterScaleType==SpectralFilterBankScale_Linear){
			float det=0;

			det=samplate/(float )fftLength;

			lowIndex=bftObj->lowIndex;
			highIndex=bftObj->highIndex;

			for(int i=lowIndex,j=0;i<=highIndex;i++,j++){
				freBandArr[j]=i*det;
				binBandArr[j]=i;
			}
		}
		else{
			auditory_filterBank(num,fftLength,samplate,0,
							filterScaleType,filterStyleType,filterNormalType,
							lowFre,highFre,binPerOctave,
							mFilterBankArr,
							freBandArr,
							binBandArr);
		}
	}

	// 3. temproal
	if(bftObj->isTemporal){
		temporalObj_new(&tempObj,&fftLength,&slideLength,&windowType);
	}

	bftObj->reassignObj=reassignObj;

	bftObj->mFilterBankArr=mFilterBankArr;
	bftObj->mArr1=mArr1;

	bftObj->freBandArr=freBandArr;
	bftObj->binBandArr=binBandArr;

	bftObj->tempObj=tempObj;
}

/***
	1. S real/complex
	2. S mag/power/p
	S.dot(filterBank) t*(fftLength/2+1) @ num*(fftLength/2+1) => t*num
	
****/
void bftObj_bft(BFTObj bftObj,float *dataArr,int dataLength,float *mRealArr3,float *mImageArr3){
	ReassignObj reassignObj=NULL;

	int fftLength=0; // fftLength,timeLength,num
	int timeLength=0;

	int num=0;
	float *mFilterBankArr=NULL;

	SpectralDataType dataType;
	SpectralFilterBankScaleType filterScaleType;

	float normValue=1;
	int resultType=0; // 0 complex 1 real->mRealArr

	float *mRealArr=NULL;
	float *mImageArr=NULL;

	int lowIndex=0; // only for linear
	int highIndex=0;

	float *mArr1=NULL;

	reassignObj=bftObj->reassignObj;

	filterScaleType=bftObj->filterScaleType;
	dataType=bftObj->dataType;

	normValue=bftObj->normValue;
	resultType=bftObj->resultType;

	fftLength=bftObj->fftLength;
	
	num=bftObj->num;

	mFilterBankArr=bftObj->mFilterBankArr; // num*(fftLength/2+1)
	mArr1=bftObj->mArr1;

	mRealArr=bftObj->mRealArr; // timeLength*fftLength
	mImageArr=bftObj->mImageArr;

	lowIndex=bftObj->lowIndex; 
	highIndex=bftObj->highIndex;

	timeLength=reassignObj_calTimeLength(reassignObj,dataLength);
	if(bftObj->timeLength<timeLength||
		bftObj->timeLength>timeLength*2){ // 更新缓存
		free(mRealArr);
		free(mImageArr);
		
		mRealArr=__vnew(timeLength*fftLength, NULL);
		mImageArr=__vnew(timeLength*fftLength, NULL);
	}

	// 1. reassign -> timeLength*(fftLength/2+1)
	reassignObj_reassign(reassignObj,dataArr,dataLength,
						mRealArr,mImageArr,
						NULL,NULL);

	// 2. dot
	if(!resultType){ // complex
		if(dataType==SpectralData_Power){
			for(int i=0;i<timeLength*(fftLength/2+1);i++){
				float r1=0;
				float i1=0;

				r1=mRealArr[i];
				i1=mImageArr[i];

				mRealArr[i]=r1*r1-i1*i1;
				mImageArr[i]=2*r1*i1;
			}
		}

		// dot
		if(filterScaleType==SpectralFilterBankScale_Linear){
			for(int i=0;i<timeLength;i++){
				for(int j=lowIndex,k=0;j<=highIndex;j++,k++){
					mRealArr3[i*num+k]=mRealArr[i*(fftLength/2+1)+j];
					mImageArr3[i*num+k]=mImageArr[i*(fftLength/2+1)+j];
				}
			}
		}
		else{
			__mcdot1(mRealArr,mImageArr,
					mFilterBankArr,mArr1,
					timeLength,fftLength/2+1,
					num,fftLength/2+1,
					mRealArr3,mImageArr3);
		}
	}
	else{
		__mcsquare(mRealArr, mImageArr, timeLength, fftLength/2+1,1, mRealArr); // S^2
		
		// S/S^2 -> norm
		if(dataType==SpectralData_Mag){

			for(int i=0;i<timeLength*(fftLength/2+1);i++){
				mRealArr[i]=sqrtf(mRealArr[i]);
			}
		}
		else if(dataType==SpectralData_Power){
			if(normValue!=1){ 
				for(int i=0;i<timeLength*(fftLength/2+1);i++){
					mRealArr[i]=powf(mRealArr[i], normValue);
				}
			}
		}

		// dot
		if(filterScaleType==SpectralFilterBankScale_Linear){
			for(int i=0;i<timeLength;i++){
				for(int j=lowIndex,k=0;j<=highIndex;j++,k++){
					mRealArr3[i*num+k]=mRealArr[i*(fftLength/2+1)+j];
				}
			}
		}
		else{
			__mdot1(mRealArr,mFilterBankArr,
					timeLength,fftLength/2+1,
					num,fftLength/2+1,
					mRealArr3);
		}
		
		// norm
		if(dataType==SpectralData_Mag){
			if(normValue!=1){
				for(int i=0;i<timeLength*num;i++){
					mRealArr3[i]=powf(mRealArr3[i],normValue);
				}
			}
		}
	}

	// 3. temporal
	if(bftObj->isTemporal){
		temporalObj_temporal(bftObj->tempObj,dataArr,dataLength);
	}

	bftObj->timeLength=timeLength;

	bftObj->mRealArr=mRealArr;
	bftObj->mImageArr=mImageArr;
}

// energy/rms/zeroCrossRate
void bftObj_getTemporalData(BFTObj bftObj,float **eArr,float **rArr,float **zArr){

	if(bftObj->tempObj){
		temporalObj_getData(bftObj->tempObj,eArr,rArr,zArr,NULL);
	}
}

int bftObj_calTimeLength(BFTObj bftObj,int dataLength){
	int timeLength=0;

	timeLength=reassignObj_calTimeLength(bftObj->reassignObj,dataLength);
	return timeLength;
}

float *bftObj_getFreBandArr(BFTObj bftObj){

	return bftObj->freBandArr;
}

int *bftObj_getBinBandArr(BFTObj bftObj){

	return bftObj->binBandArr;
}

// 0 complex,1 real ->mRealArr
void bftObj_setResultType(BFTObj bftObj,int type){

	bftObj->resultType=type;
}

void bftObj_setDataNormValue(BFTObj bftObj,float normValue){

	if(normValue>0){
		bftObj->normValue=normValue;
	}
}

void bftObj_free(BFTObj bftObj){
	ReassignObj reassignObj=NULL;

	float *mFilterBankArr=NULL; // num*(fftLength/2+1)

	float *freBandArr=NULL;
	int *binBandArr=NULL;

	float *mRealArr=NULL; // rea r,i(timeLength*(fftLength/2+1)) -> power r(timeLength*(fftLength/2+1)) 
	float *mImageArr=NULL;

	float *mArr1=NULL; 

	TemporalObj tempObj=NULL;

	if(bftObj){
		reassignObj=bftObj->reassignObj;

		mFilterBankArr=bftObj->mFilterBankArr;

		freBandArr=bftObj->freBandArr;
		binBandArr=bftObj->binBandArr;

		mRealArr=bftObj->mRealArr;
		mImageArr=bftObj->mImageArr;

		mArr1=bftObj->mArr1;

		tempObj=bftObj->tempObj;

		reassignObj_free(reassignObj);

		free(mFilterBankArr);

		free(freBandArr);
		free(binBandArr);

		free(mRealArr);
		free(mImageArr);

		free(mArr1);

		temporal_free(tempObj);

		free(bftObj);
	}
}










```

---

### Archivo: `./src/stft_algorithm.h`

```


#ifndef STFT_ALGORITHM_H
#define STFT_ALGORITHM_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "flux_base.h"

typedef struct OpaqueSTFT *STFTObj;

int stftObj_new(STFTObj *stftObj,int radix2Exp,WindowType *windowType,int *slideLength,int *isContinue);

void stftObj_setSlideLength(STFTObj stftObj,int slideLength);
// value1 => constant/left
void stftObj_setPadding(STFTObj stftObj,
					PaddingPositionType *positionType,PaddingModeType *modeType,
					float *value1,float *value2);

void stftObj_useWindowDataArr(STFTObj stftObj,float *winDataArr);
float *stftObj_getWindowDataArr(STFTObj stftObj);

// center zero padding
void stftObj_enablePadding(STFTObj stftObj,int flag);
void stftObj_enableContinue(STFTObj stftObj,int flag);

// set/enable后执行
int stftObj_calTimeLength(STFTObj stftObj,int dataLength);
int stftObj_calDataLength(STFTObj stftObj,int timeLength);

void stftObj_stft(STFTObj stftObj,float *dataArr,int dataLength,float *mRealArr,float *mImageArr);
// type 0(deault) 'weight overlap-add' 1 'overlap-add'
void stftObj_istft(STFTObj stftObj,float *mRealArr,float *mImageArr,int nLength,int type,float *dataArr);

void stftObj_free(STFTObj stftObj);
void stftObj_debug(STFTObj stftObj);

#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/CMakeLists.txt`

```
cmake_minimum_required(VERSION 3.5)
project(audioflux-redux)

# Definimos explícitamente solo los archivos que vamos a compilar
set(SOURCES
    # Archivos en la raíz de src/
    bft_algorithm.c
    cqt_algorithm.c
    flux_spectral.c   # Necesario para onset
    flux_temporal.c   # Necesario para bft
    reassign_algorithm.c
    stft_algorithm.c
    
    # Archivos en dsp/
    dsp/fft_algorithm.c
    dsp/flux_window.c
    dsp/flux_correct.c # Necesario para reassign (usado en bft)
    dsp/phase_vocoder.c # Necesario para reassign (usado en bft)

    # Archivos en filterbank/
    filterbank/auditory_filterBank.c
    filterbank/cqt_filterBank.c
    
    # Archivos en mir/
    mir/onset_algorithm.c
    mir/_queue.c

    # Archivos en util/
    util/flux_util.c
    util/flux_wave.c
    
    # Archivos en vector/
    vector/flux_complex.c
    vector/flux_vector.c
    vector/flux_vectorInt.c
    vector/flux_vectorOp.c
)

if(${CMAKE_SYSTEM_NAME} MATCHES "iOS")
	set(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -DHAVE_ACCELERATE")

	# set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -s")

	add_library(audioflux
				${SOURCES})

	target_link_libraries(audioflux
						"-framework Accelerate")

	install(TARGETS audioflux DESTINATION lib)

elseif (${CMAKE_SYSTEM_NAME} MATCHES "darwin")
	set(CMAKE_C_COMPILER $ENV{C_COMPILER_PATH})
	set(CMAKE_CXX_COMPILER $ENV{CXX_COMPILER_PATH})
	if (DEFINED ENV{AF_BUILD_PY_BDIST})
		message("Build py_bdist version")

		set(ompPath ../scripts/macOS/openmp)
		include_directories(${ompPath})
		link_directories(${ompPath})
	endif()

	set(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -O3 -DHAVE_ACCELERATE -DHAVE_OMP -fopenmp ")

	add_library(audioflux
				SHARED
				${SOURCES})

	target_link_libraries(audioflux
						"-framework Accelerate"
						omp
						)

	install(TARGETS audioflux DESTINATION lib)

elseif (${CMAKE_SYSTEM_NAME} MATCHES "android")
	set(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -std=c99  -DHAVE_FFTW3F ")

	# strip
	set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -s")

	if(${CMAKE_ANDROID_ARCH_ABI} MATCHES "armeabi-v7a")
		set(fftwPath ../scripts/android/fftw3/armeabi-v7a)
	elseif(${CMAKE_ANDROID_ARCH_ABI} MATCHES "arm64-v8a")
		set(fftwPath ../scripts/android/fftw3/arm64-v8a)
	elseif(${CMAKE_ANDROID_ARCH_ABI} MATCHES "armeabi")
		set(fftwPath ../scripts/android/fftw3/armeabi)
	endif()

	include_directories(${fftwPath})
	link_directories(${fftwPath})

	# add dylib, include source path
	add_library(audioflux
				SHARED
				${SOURCES})

	# search system lib, ndk-10e is not support
	find_library( # Sets the name of the path variable.
				syslibs
				log
				android)

	# link target lib
	target_link_libraries(audioflux
						 fftw3f
						 log)

	install(TARGETS audioflux DESTINATION lib)

elseif (${CMAKE_SYSTEM_NAME} MATCHES "linux")
	set(CMAKE_C_COMPILER "/usr/bin/clang")
	set(CMAKE_CXX_COMPILER "/usr/bin/clang++")
	if (DEFINED ENV{AF_BUILD_PY_BDIST})
		message("Build py_bdist version")
		set(OMP_PATH "../scripts/linux/openmp")
		set(MKL_INCLUDE_PATH "../scripts/linux/mkl/include")
		set(MKL_LIB_PATH "../scripts/linux/mkl")

		include_directories(${OMP_PATH})
		link_directories(${OMP_PATH})
	else()
		set(MKL_INCLUDE_PATH $ENV{MKL_INCLUDE_PATH})
		set(MKL_LIB_PATH $ENV{MKL_LIB_PATH})
	endif()

    message("Using MKL_INCLUDE_PATH: ${MKL_INCLUDE_PATH}")
    message("Using MKL_LIB_PATH: ${MKL_LIB_PATH}")

	if (MKL_LIB_PATH)
		set(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -O3 -DHAVE_MKL -DHAVE_OMP -fopenmp=libomp -Wl,-rpath,${MKL_LIB_PATH} ")
	else()
		set(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -O3 -DHAVE_OMP -fopenmp=libomp ")
	endif()

	if (MKL_INCLUDE_PATH)
		include_directories(${MKL_INCLUDE_PATH})
	endif()
	if (MKL_LIB_PATH)
		link_directories(${MKL_LIB_PATH})
	endif()
	include_directories(${PROJECT_SOURCE_DIR})
	link_directories(${PROJECT_SOURCE_DIR})

	# add so, include source path
	add_library(audioflux
				SHARED
				${SOURCES})

	# link target lib
	if (MKL_LIB_PATH)
        target_link_libraries(audioflux
						      mkl_intel_lp64
						      mkl_core
						      mkl_intel_thread
						      omp
						      m)
    else()
        target_link_libraries(audioflux
                              omp
                              m)
	endif()


	install(TARGETS audioflux DESTINATION lib)

elseif (${CMAKE_SYSTEM_NAME} MATCHES "win64")
	# -Wl,-rpath=.
	# -Wl,--out-implib,./audioflux.lib  MSVC lib
	set(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -DHAVE_FFTW3F -Wl,-rpath=.  ")

	set(BUILD_SHARED_LIBS true)
	set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS true)

	set(fftwPath ../scripts/windows/fftw3)
	include_directories(${fftwPath})

	link_directories(${PROJECT_SOURCE_DIR})
	include_directories(${PROJECT_SOURCE_DIR})

	# add so, include source path
	add_library(audioflux
				SHARED
				${SOURCES})

	# link target lib
	target_link_libraries(audioflux
						 fftw3f-3
						 )

	install(TARGETS audioflux DESTINATION lib)

endif()







```

---

### Archivo: `./src/flux_spectral.c`

```
// 

#include <string.h>
#include <math.h>

#include "vector/flux_vector.h"
#include "vector/flux_complex.h"

#include "flux_spectral.h"

static void __spectral_pd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
						int *indexArr,int indexLength,
						int isWeight,int isNorm,
						float *vArr);

static void __spectral_cd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
						int *indexArr,int indexLength,
						int isRectify,
						float *vArr);

void spectral_flatness(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,
					float *vArr){
	double n1=1;
	float m1=0;

	for(int i=0;i<nLength;i++){
		// n1=1;	
		// for(int j=start;j<=end;j++){
		// 	n1*=mDataArr[i*mLength+j];
		// }

		// convert log
		n1=0;	
		for(int j=0;j<indexLength;j++){
			int _index=0;

			_index=indexArr[j];
			n1+=logf(mDataArr[i*mLength+_index]+2.0e-16);
		}

		// n1=powf(n1, 1.0/(end-start));
		n1=n1/indexLength;
		n1=expf(n1);
		m1=sumArr[i]/indexLength;

		if(m1){
			vArr[i]=n1/m1; // m1 eps ???
		}
		else{
			vArr[i]=0;
		}
	}
}

// step>=1 isExp 0 type 0 sum 1 mean 
void spectral_flux(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					int step,float p,int isPostive,int isExp,int type,
					float *vArr){
	float value=0;

	if(step<1){
		step=1;
	}

	memset(vArr, 0, sizeof(float )*step);
	for(int i=step;i<nLength;i++){
		value=0;
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=mDataArr[i*mLength+_index]-mDataArr[(i-step)*mLength+_index];
			if(isPostive){
				v1=(v1>0?v1:0);
			}
			else{
				v1=fabsf(v1);
			}

			if(p==2.0){
				v1*=v1;
			}
			else{
				v1=powf(v1, p);
			}
			
			value+=v1;
		}

		if(type){ // mean
			value/=indexLength;
		}

		if(isExp){
			vArr[i]=powf(value, 1.0/p); 
		}
		else{
			vArr[i]=value;
		}
	}
}

void spectral_rolloff(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,float threshold,
					float *vArr){
	float n1=0;
	float m1=0;

	int index=0;

	for(int i=0;i<nLength;i++){
		n1=0;	
		m1=sumArr[i]*threshold;
		for(int j=0;j<indexLength;j++){
			float v=0;
			int _index=0;

			_index=indexArr[j];
			v=fabsf(mDataArr[i*mLength+_index]);
			n1+=v;
			if(n1>=m1){
				// float d1=0;
				// float d2=0;

				// d1=n1-m1;
				// d2=m1-(n1-v);
				// if(d1<d2){
				// 	index=j;
				// }
				// else{
				// 	index=(j-1<start?start:j-1);
				// }

				index=_index;
				break;
			}
		}

		vArr[i]=freArr[index]; // m1 eps ???
	}
}

void spectral_centroid(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,
					float *vArr){
	float n1=0;
	float m1=0;

	for(int i=0;i<nLength;i++){
		n1=0;	
		m1=sumArr[i];
		for(int j=0;j<indexLength;j++){
			int _index=0;

			_index=indexArr[j];
			n1+=freArr[_index]*mDataArr[i*mLength+_index];
			// m1+=mDataArr[i*mLength+j];
		}

		if(m1){
			vArr[i]=n1/m1; // m1 eps ???
		}
		else{
			vArr[i]=0;
		}
	}
}

void spectral_spread(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,float *cArr,
					float *vArr){
	float n1=0;
	float m1=0;

	for(int i=0;i<nLength;i++){
		n1=0;	
		m1=sumArr[i];
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=(freArr[_index]-cArr[i]);
			n1+=v1*v1*
				mDataArr[i*mLength+_index];
		}

		if(m1){
			vArr[i]=sqrtf(n1/m1); // m1 eps ???
		}
		else{
			vArr[i]=0;
		}
	}
}

void spectral_skewness(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,float *cArr1,float *cArr2,
					float *vArr){
	float n1=0;
	float m1=0;

	for(int i=0;i<nLength;i++){
		n1=0;	
		m1=cArr2[i]*cArr2[i]*cArr2[i]*sumArr[i];
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=(freArr[_index]-cArr1[i]);
			n1+=v1*v1*v1*
				mDataArr[i*mLength+_index];
		}

		if(m1){
			vArr[i]=n1/m1; // m1 eps ???
		}
		else{
			vArr[i]=0;
		}
	}
}

void spectral_kurtosis(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,float *cArr1,float *cArr2,
					float *vArr){
	float n1=0;
	float m1=0;

	for(int i=0;i<nLength;i++){
		n1=0;	
		m1=cArr2[i]*cArr2[i]*cArr2[i]*cArr2[i]*sumArr[i];
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=(freArr[_index]-cArr1[i]);
			n1+=v1*v1*v1*v1*
				mDataArr[i*mLength+_index];
		}

		if(m1){
			vArr[i]=n1/m1; // m1 eps ???
		}
		else{
			vArr[i]=0;
		}
	}
}

void spectral_entropy(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *sumArr,int isNorm,
					float *vArr){
	float n1=0;
	float m1=0;

	for(int i=0;i<nLength;i++){
		n1=0;	
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=mDataArr[i*mLength+_index]/sumArr[i];
			n1+=v1*log2f(v1+1e-16);
		}

		if(isNorm){ // matlab
			m1=log2f(indexLength);
			if(m1){
				vArr[i]=-n1/m1; // m1 eps ???
			}
			else{
				vArr[i]=0;
			}
		}
		else{ // song
			vArr[i]=-n1;
		}
	}
}

void spectral_crest(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,
					float *vArr){
	float n1=0;
	float m1=0;

	for(int i=0;i<nLength;i++){
		n1=mDataArr[i*mLength+indexArr[0]];	
		m1=sumArr[i]/indexLength;
		for(int j=1;j<indexLength;j++){
			int _index=0;

			_index=indexArr[j];
			if(n1<mDataArr[i*mLength+_index]){
				n1=mDataArr[i*mLength+_index];
			}
		}

		if(m1){
			vArr[i]=n1/m1; // m1 eps ???
		}
		else{
			vArr[i]=0;
		}
	}
}

void spectral_slope(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *meanFreArr,float *meanValueArr,
					float *vArr){
	float n1=0;
	float m1=0;

	for(int i=0;i<nLength;i++){
		n1=0;	
		m1=0;
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=(freArr[_index]-meanFreArr[i]);
			n1+=v1*(mDataArr[i*mLength+_index]-meanValueArr[i]);
			m1+=v1*v1;
		}

		if(m1){
			vArr[i]=n1/m1; // m1 eps ???
		}
		else{
			vArr[i]=0;
		}
	}
}

void spectral_decrease(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *sumArr,
					float *vArr){
	float n1=0;
	float m1=0;

	for(int i=0;i<nLength;i++){
		n1=0;
		m1=sumArr[i]-mDataArr[i*mLength+indexArr[0]];	
		for(int j=1;j<indexLength;j++){
			int _index=0;

			_index=indexArr[j];
			n1+=(mDataArr[i*mLength+_index]-mDataArr[i*mLength+indexArr[0]])/(_index);
		}

		if(m1){
			vArr[i]=n1/m1; // m1 eps ???
		}
		else{
			vArr[i]=0;
		}
	}
}

void spectral_bandWidth(float *mDataArr,int nLength,int mLength,
						int *indexArr,int indexLength,
						float *freArr,float *cArr,float p,
						float *vArr){
	float value1=0;

	for(int i=0;i<nLength;i++){
		value1=0;	
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=(freArr[_index]-cArr[i]);
			if(p==2.0){
				v1*=v1;
			}
			else{
				v1=powf(v1, p);
			}

			value1+=(mDataArr[i*mLength+_index]*v1);
		}

		if(p!=1.0){
			value1=powf(value1, 1.0/p);
		}
		vArr[i]=value1;
	}
}

void spectral_rms(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr){
	float value1=0;

	for(int i=0;i<nLength;i++){
		value1=0;	
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=mDataArr[i*mLength+_index];
			v1*=v1;
			if(_index==0||
				(mLength%2==0&&_index==mLength-1)){
				
				v1*=0.5;
			}

			value1+=v1;
		}

		value1=sqrtf(2*value1/(mLength*mLength));
		vArr[i]=value1;
	}
}

// ['hfc', 'sd', 'sf', 'mkl', 'pd', 'wpd', 'nwpd', 'cd', 'rcd']
// type 0 sum 1 mean
void spectral_hfc(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr){
	float value=0;

	vArr[0]=0;
	for(int i=0;i<nLength;i++){
		value=0;
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=mDataArr[i*mLength+_index]*_index;
			value+=v1;
		}

		vArr[i]=value;
	}
}

// sum(diff); positive=1
void spectral_sd(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				int step,int isPostive,
				float *vArr){
	float value=0;

	if(step<1){
		step=1;
	}
	
	memset(vArr, 0, sizeof(float )*step);
	for(int i=step;i<nLength;i++){
		value=0;
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=mDataArr[i*mLength+_index]-mDataArr[(i-step)*mLength+_index];
			if(isPostive){
				v1=(v1>0?v1:0);
			}
			else{
				v1=fabsf(v1);
			}

			value+=v1;
		}

		vArr[i]=value;
	}
}

// sum(diff^2); positive=1
void spectral_sf(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				int step,int isPostive,
				float *vArr){
	float value=0;

	if(step<1){
		step=1;
	}

	memset(vArr, 0, sizeof(float )*step);
	for(int i=step;i<nLength;i++){
		value=0;
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=mDataArr[i*mLength+_index]-mDataArr[(i-step)*mLength+_index];
			if(isPostive){
				v1=(v1>0?v1:0);
			}
			else{
				v1=fabsf(v1);
			}

			value+=v1*v1;
		}

		vArr[i]=value; 
	}
}

// type 0 sum 1 mean
void spectral_mkl(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				int type,
				float *vArr){
	float value=0;

	vArr[0]=0;
	for(int i=1;i<nLength;i++){
		value=0;
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=mDataArr[i*mLength+_index]/(mDataArr[(i-1)*mLength+_index]+1e-16);
			// log compress
			v1=logf(1+v1);
			value+=v1;
		}

		if(type){
			value/=indexLength;
		}

		vArr[i]=value;
	}
}

static void __spectral_pd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
						int *indexArr,int indexLength,
						int isWeight,int isNorm,
						float *vArr){
	float value=0;

	vArr[0]=0;
	for(int i=2;i<nLength;i++){
		value=0;
		for(int j=0;j<indexLength;j++){
			float v1=0;
			int _index=0;

			_index=indexArr[j];
			v1=mPhaseArr[i*mLength+_index]-2*mPhaseArr[(i-1)*mLength+_index]+mPhaseArr[(i-2)*mLength+_index];
			// 0~2pi --> -pi~pi
			
			v1=fabsf(v1);
			if(isWeight||isNorm){
				v1=v1*mSpecArr[i*mLength+_index];
			}

			value+=v1;
		}

		value/=indexLength;
		if(isNorm){
			float _m1=0;

			for(int j=0;j<indexLength;j++){
				int _index=0;

				_index=indexArr[j];
				_m1+=mSpecArr[i*mLength+_index];
			}
			_m1=_m1/indexLength;

			value=value/(_m1+1e-16);
		}

		vArr[i]=value;
	}
}

void spectral_pd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr){
	
	__spectral_pd(mSpecArr,mPhaseArr,nLength,mLength,
				indexArr,indexLength,
				0,0,
				vArr);
}

void spectral_wpd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr){

	__spectral_pd(mSpecArr,mPhaseArr,nLength,mLength,
				indexArr,indexLength,
				1,0,
				vArr);
}

void spectral_nwpd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr){

	__spectral_pd(mSpecArr,mPhaseArr,nLength,mLength,
				indexArr,indexLength,
				0,1,
				vArr);
}

static void __spectral_cd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
						int *indexArr,int indexLength,
						int isRectify,
						float *vArr){
	float value=0;

	vArr[0]=0;
	for(int i=1;i<nLength;i++){
		value=0;
		for(int j=0;j<indexLength;j++){
			float v1=0;
			float v2=0;

			float real1=0;
			float image1=0;

			float real2=0;
			float image2=0;

			int _index=0;

			_index=indexArr[j];

			if(isRectify){
				if(mSpecArr[i*mLength+_index]<=mSpecArr[(i-1)*mLength+_index]){
					continue;
				}
			}

			v1=mPhaseArr[i*mLength+_index];
			real1=mSpecArr[i*mLength+_index]*cosf(v1);
			image1=mSpecArr[i*mLength+_index]*sin(v1);

			if(i>1){
				v2=2*mPhaseArr[(i-1)*mLength+_index]-mPhaseArr[(i-2)*mLength+_index];
				
				real2=mSpecArr[(i-1)*mLength+_index]*cosf(v2);
				image2=mSpecArr[(i-1)*mLength+_index]*sin(v2);

				real1-=real2;
				image1-=image2;
			}
			
			v1=sqrtf(real1*real1+image1*image1);
			value+=v1;
		}

		vArr[i]=value;
	}
}

void spectral_cd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr){

	__spectral_cd(mSpecArr,mPhaseArr,nLength,mLength,
				indexArr,indexLength,
				0,
				vArr);
}

void spectral_rcd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr){

	__spectral_cd(mSpecArr,mPhaseArr,nLength,mLength,
				indexArr,indexLength,
				1,
				vArr);
}

// threshold 0/3/6...
void spectral_broadband(float *mDataArr,int nLength,int mLength,
						int *indexArr,int indexLength,
						float threshold,
						float *vArr){
	vArr[0]=0;
	for(int i=1;i<nLength;i++){
		for(int j=0;j<indexLength;j++){
			float diff=0;
			int _index=0;

			_index=indexArr[j];
			diff=10.0*log10f(mDataArr[i*mLength+_index]/(mDataArr[(i-1)*mLength+_index]));
			if(diff>threshold){
				vArr[i]++;
			}
		}
	}
}

/***
	step >=1
	threshold 0
	methodType 'sub'
	dataType 'value'
****/
void spectral_novelty(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					int step,float threshold,
					SpectralNoveltyMethodType *methodType,SpectralNoveltyDataType *dataType,
					float *vArr){
	float value=0;

	SpectralNoveltyMethodType mType=SpectralNoveltyMethod_Sub;
	SpectralNoveltyDataType dType=SpectralNoveltyData_Value;

	if(methodType){
		mType=*methodType;
	}

	if(dataType){
		dType=*dataType;
	}

	if(step<1){
		step=1;
	}

	memset(vArr, 0, sizeof(float )*step);
	for(int i=step;i<nLength;i++){
		value=0;
		for(int j=0;j<indexLength;j++){
			float pre=0;
			float cur=0;

			float v1=0;
			int _index=0;

			_index=indexArr[j];

			cur=mDataArr[i*mLength+_index];
			pre=mDataArr[(i-step)*mLength+_index];

			if(mType==SpectralNoveltyMethod_Sub){
				v1=cur-pre;
			}
			else if(mType==SpectralNoveltyMethod_Entroy){
				v1=logf(cur/(pre+1e-16));
			}
			else if(mType==SpectralNoveltyMethod_KL){
				v1=cur*logf(cur/(pre+1e-16));
			}
			else{ // IS
				v1=cur/(pre+1e-16)-logf(cur/(pre+1e-16))-1;
			}

			if(dType==SpectralNoveltyData_Value){
				if(v1>threshold){
					value+=v1;
				}
			}
			else{ // Number
				if(v1>threshold){
					value++;
				}
			}
		}

		vArr[i]=value;
	}
}

void spectral_energy(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					int isPower,int isLog,float gamma,
					float *vArr){
	for(int i=0;i<nLength;i++){
		vArr[i]=0;
		for(int j=0;j<indexLength;j++){
			float _value=0;
			int _index=0;

			_index=indexArr[j];
			_value=mDataArr[i*mLength+_index];
			if(!isPower){
				_value*=_value;
			}

			if(isLog){
				if(gamma<=0){
					gamma=10;
				}

				_value=logf(1+gamma*_value);
			}

			vArr[i]+=_value;
		}

		vArr[i]/=indexLength; // fre domain ???
	}	
}











```

---

### Archivo: `./src/reassign_algorithm.c`

```
// clang 

#include <string.h>
#include <math.h>

#include "vector/flux_vector.h"
#include "vector/flux_vectorOp.h"
#include "vector/flux_complex.h"

#include "util/flux_util.h"

#include "dsp/flux_window.h"

#include "stft_algorithm.h"
#include "reassign_algorithm.h"

struct OpaqueReassign{
	int isContinue; 

	ReassignType resType;
	int isPadding;
	
	int samplate;
	STFTObj stftObj; // 基于STFT linear的reassign ???
	
	int slideLength;
	int fftLength; 
	int timeLength;

	float *freArr;  // fftLength/2+1
	float *timeArr; // timeLength

	float *mReFreArr; // timeLength*(fftLength/2+1)
	float *mReTimeArr;

	// win数据相关 fftLength
	float *winArr; // S_h
	float *winDerivativeArr; // S_dh +1
	float *winWeightArr; // s_th

	// stft相关 timeLength*fftLength => timeLength*(fftLength/2+1)
	float *mRealArr1; // S_h
	float *mImageArr1;

	float *mRealArr2; // S_dh
	float *mImageArr2;

	float *mRealArr3; // S_th
	float *mImageArr3;

	// rearrage相关 timeLength*(fftLength/2+1)
	int *mTimeIndexArr;
	int *mFreIndexArr;

	int *mTempIndexArr;

	float thresh; // 0.001

	int resultType; // 0 complex 1 mRealArr1 -> amp
	int order; // >=1 

};

static void _reassignObj_initWindowData(ReassignObj reassignObj);

static void _reassignObj_dealTCorrData(ReassignObj reassignObj,int dataLength);

static void _reassignObj_stft(ReassignObj reassignObj,float *dataArr,int dataLength);
static void _reassignObj_reassignTimeFre(ReassignObj reassignObj,float *dataArr,int dataLength);
static void _reassignObj_filterTimeFre(ReassignObj reassignObj,int dataLength);
static void _reassignObj_rearrage(ReassignObj reassignObj,float *mRealArr4,float *mImageArr4,float *mRealArr5,float *mImageArr5);

/***
	radix2Exp 12
	samplate 32000
	windowType 'hann'
	slideLength fftLength/4

	reType Reassign_All
	thresh 0.001 

	isPadding 0
	isContinue 0
****/
int reassignObj_new(ReassignObj *reassignObj,int radix2Exp,
					int *samplate,WindowType *windowType,int *slideLength,
					ReassignType *reType,float *thresh,
					int *isPadding,int *isContinue){
	int status=0;
	ReassignObj re=NULL;

	ReassignType _resType=Reassign_All;
	int _samplate=32000;
	int _isPadding=0;

	int _radix2Exp=12;
	WindowType _windowType=Window_Hann;
	int _slideLength=0;
	int _isContinue=0;

	STFTObj stftObj=NULL;

	int fftLength=0;

	float *freArr=NULL;  // fftLength/2+1

	float _thresh=0.001;

	re=*reassignObj=(ReassignObj )calloc(1, sizeof(struct OpaqueReassign ));

	if(reType){
		_resType=*reType;
	}

	if(samplate){
		if(*samplate>0){
			_samplate=*samplate;
		}
	}

	if(isPadding){
		_isPadding=*isPadding;
	}

	if(radix2Exp>1&&radix2Exp<31){
		_radix2Exp=radix2Exp;
	}

	if(windowType){
		_windowType=*windowType;
	}

	fftLength=(1<<_radix2Exp);
	if(slideLength){
		if(*slideLength>0){
			_slideLength=*slideLength;
		}
	}

	if(!_slideLength){
		_slideLength=fftLength/4;
	}

	if(thresh){
		if(*thresh>=0){
			_thresh=*thresh;
		}
	}

	stftObj_new(&stftObj, _radix2Exp, &_windowType, &_slideLength, &_isContinue);
	stftObj_enablePadding(stftObj, _isPadding);

	re->isContinue=_isContinue;

	re->resType=_resType;
	re->isPadding=_isPadding;

	re->samplate=_samplate;
	re->stftObj=stftObj;

	re->slideLength=_slideLength;
	re->fftLength=fftLength;

	re->thresh=_thresh;

	// init winArr相关
	_reassignObj_initWindowData(re);

	// fre相关
	freArr=__vlinspace(0, _samplate/2.0, fftLength/2+1, 0);
	re->freArr=freArr;

	return status;
}

int reassignObj_calTimeLength(ReassignObj reassignObj,int dataLength){

	return stftObj_calTimeLength(reassignObj->stftObj, dataLength);
}

// 0 complex,1 mRealArr1 -> amp
void reassignObj_setResultType(ReassignObj reassignObj,int type){

	reassignObj->resultType=type;
}

// order >=1
void reassignObj_setOrder(ReassignObj reassignObj,int order){

	reassignObj->order=order;
}

/***
	1. tcorr
	2. stft => S_h
	3. stft => S_dh&S_th
	4. filter tcorr/fcorr 
	5. rearrage 
****/
void reassignObj_reassign(ReassignObj reassignObj,float *dataArr,int dataLength,
						float *mRealArr4,float *mImageArr4,
						float *mRealArr5,float *mImageArr5){
	if(reassignObj->resType!=Reassign_None){
		// 1. tcorr
		_reassignObj_dealTCorrData(reassignObj, dataLength);

		// 2. S_h
		_reassignObj_stft(reassignObj, dataArr, dataLength);

		// 3. S_dh&S_th
		_reassignObj_reassignTimeFre(reassignObj,dataArr,dataLength);

		// 4. filter
		_reassignObj_filterTimeFre(reassignObj,dataLength);

		// 5. rearrage
		_reassignObj_rearrage(reassignObj,mRealArr4,mImageArr4,mRealArr5,mImageArr5);
	}
	else{
		int fftLength=0; 
		int timeLength=0;

		float *mRealArr1=NULL; // S_h
		float *mImageArr1=NULL;

		fftLength=reassignObj->fftLength;
		timeLength=reassignObj->timeLength;

		mRealArr1=reassignObj->mRealArr1;
		mImageArr1=reassignObj->mImageArr1;

		timeLength=stftObj_calTimeLength(reassignObj->stftObj,dataLength);
		if(reassignObj->timeLength<timeLength||
			reassignObj->timeLength>timeLength*2){
			free(mRealArr1);
			free(mImageArr1);

			mRealArr1=__vnew(timeLength*fftLength, NULL);
			mImageArr1=__vnew(timeLength*fftLength, NULL);

			reassignObj->timeLength=timeLength;
			reassignObj->mRealArr1=mRealArr1;
			reassignObj->mImageArr1=mImageArr1;
		}

		_reassignObj_stft(reassignObj, dataArr, dataLength);

		memcpy(mRealArr4, mRealArr1, sizeof(float )*timeLength*(fftLength/2+1));
		memcpy(mImageArr4, mImageArr1, sizeof(float )*timeLength*(fftLength/2+1));
	}

}

/***
	fre*timeLength -->timeLength*fre
	rearrage use mag^2/(∑win^2) or mag/power???
****/
static void _reassignObj_rearrage(ReassignObj reassignObj,float *mRealArr4,float *mImageArr4,float *mRealArr5,float *mImageArr5){
	int fftLength=0; 
	int timeLength=0;

	float *freArr=NULL;  // fftLength/2+1
	float *timeArr=NULL;

	float *mReFreArr=NULL; // timeLength*(fftLength/2+1)
	float *mReTimeArr=NULL;

	float *mRealArr1=NULL; // S_h
	float *mImageArr1=NULL;

	int *mTimeIndexArr=NULL; 
	int *mFreIndexArr=NULL;

	int *mTempIndexArr=NULL;

	int order=1;

	int totalLength=0; // timeLength*(fftLength/2+1);

	float fmin=0;
	float fmax=0;

	float tmin=0;
	float tmax=0;

	fftLength=reassignObj->fftLength;
	timeLength=reassignObj->timeLength;

	freArr=reassignObj->freArr;
	timeArr=reassignObj->timeArr;

	mReFreArr=reassignObj->mReFreArr;
	mReTimeArr=reassignObj->mReTimeArr;

	mRealArr1=reassignObj->mRealArr1;
	mImageArr1=reassignObj->mImageArr1;

	mTimeIndexArr=reassignObj->mTimeIndexArr;
	mFreIndexArr=reassignObj->mFreIndexArr;

	mTempIndexArr=reassignObj->mTempIndexArr;

	totalLength=timeLength*(fftLength/2+1);

	order=reassignObj->order;

	fmin=freArr[0];
	fmax=freArr[fftLength/2];

	tmin=timeArr[0];
	tmax=timeArr[timeLength-1];

	// memset(rowIndexArr, 0, sizeof(int )*totalLength);
	if(timeLength>1){
		for(int i=0;i<totalLength;i++){
			mTimeIndexArr[i]=roundf((mReTimeArr[i]-tmin)*(timeLength-1)/(tmax-tmin));
		}
	}

	for(int i=0;i<totalLength;i++){
		mFreIndexArr[i]=roundf((mReFreArr[i]-fmin)*(fftLength/2)/(fmax-fmin));
	}

	// debug
	{
		// printf("mReFreArr is:\n");
		// __mdebug(mReFreArr, timeLength, fftLength/2+1, 1);
		// printf("\n");

		// printf("mReTimeArr is:\n");
		// __mdebug(mReTimeArr, timeLength, fftLength/2+1, 1);
		// printf("\n");

		// printf("timeArr is :\n");
		// __vdebug(timeArr, timeLength, 1);
		// printf("\n");

		// printf("freArr is :\n");
		// __vdebug(freArr, fftLength/2+1, 1);
		// printf("\n");

		// printf("mFreIndexArr is:\n");
		// __mdebugi(mFreIndexArr, timeLength, fftLength/2+1, 1);
		// printf("\n");
	}

	// order
	if(order>1){
		int v=0;

		memset(mTempIndexArr,0,sizeof(int )*totalLength);
		for(int k=0;k<reassignObj->order-1;k++){

			for(int i=0;i<timeLength;i++){
				for(int j=0;j<fftLength/2+1;j++){
					
					v=mFreIndexArr[i*(fftLength/2+1)+j];
					if(v>=0&&v<fftLength/2+1){
						mTempIndexArr[i*(fftLength/2+1)+j]=mFreIndexArr[i*(fftLength/2+1)+v];
					}
				}
			}

			memcpy(mFreIndexArr, mTempIndexArr, sizeof(int )*timeLength*(fftLength/2+1));
			// memset(mTempIndexArr,0,sizeof(int )*timeLength*(fftLength/2+1));
		}
	}
	
	/***
		1. abs/power,df&dt
		2. complex,df&timeArr,modified stft,  
	****/
	for(int i=0;i<timeLength;i++){
		int i1=0;
		int j1=0;

		float v1=0;
		float v2=0;

		for(int j=0;j<fftLength/2+1;j++){
			i1=mTimeIndexArr[i*(fftLength/2+1)+j];
			j1=mFreIndexArr[i*(fftLength/2+1)+j];

			v1=mRealArr1[i*(fftLength/2+1)+j];
			v2=mImageArr1[i*(fftLength/2+1)+j];

			if(j%2==1){
				v1=-v1;
				v2=-v2;
			}

			if(i1>=0&&i1<timeLength&&
				j1>=0&&j1<fftLength/2+1){

				if(!reassignObj->resultType){ // complex
					mRealArr4[i1*(fftLength/2+1)+j1]+=v1;
					mImageArr4[i1*(fftLength/2+1)+j1]+=v2;
				}
				else{ // mRealArr1 -> amp
					mRealArr4[i1*(fftLength/2+1)+j1]+=sqrtf(v1*v1+v2*v2);
				}
			}
		}
	}

	if(mRealArr5){
		memcpy(mRealArr5, mRealArr1, sizeof(float )*totalLength);
	}

	if(mImageArr5){
		memcpy(mImageArr5, mImageArr1, sizeof(float )*totalLength);
	}

}

// stft创建之后调用
static void _reassignObj_initWindowData(ReassignObj reassignObj){
	float *winArr=NULL; // S_h
	float *winDerivativeArr=NULL;
	float *winWeightArr=NULL;

	int fftLength=0;

	float *_winArr=NULL;
	float *_derArr=NULL;

	fftLength=reassignObj->fftLength;

	// 1. winArr
	winArr=__vnew(fftLength, NULL);
	_winArr=stftObj_getWindowDataArr(reassignObj->stftObj);
	memcpy(winArr, _winArr, sizeof(float )*fftLength);

	// 2. winDerivativeArr =dw(n)/dn
	winDerivativeArr=__vnew(fftLength+2, NULL);
	_derArr=__vnew(fftLength+2, NULL);
	memcpy(_derArr+1, _winArr, sizeof(float )*fftLength);
	// 'wrap' ??? 'zero'
	_derArr[0]=_derArr[fftLength];
	_derArr[fftLength+1]=_derArr[1];

	__vgradient(_derArr, fftLength+2, 1, winDerivativeArr);

	// 3. winWeightArr =n.*w(n)
	__varange(-fftLength/2, fftLength/2+1, 1, &winWeightArr);
	__vmul(winWeightArr, winArr, fftLength, winWeightArr);

	reassignObj->winArr=winArr;
	reassignObj->winDerivativeArr=winDerivativeArr; // ???
	reassignObj->winWeightArr=winWeightArr;

	free(_derArr);
}

// timeLength correlation相关数据 xcorr =>tcorr
static void _reassignObj_dealTCorrData(ReassignObj reassignObj,int dataLength){
	int timeLength=0;
	int fftLength=0;

	float *timeArr=NULL; // timeLength
	
	float *mReFreArr=NULL; // timeLength*(fftLength/2+1)
	float *mReTimeArr=NULL;

	float *mRealArr1=NULL; // S_h
	float *mImageArr1=NULL;

	float *mRealArr2=NULL; // S_dh
	float *mImageArr2=NULL;

	float *mRealArr3=NULL; // S_th
	float *mImageArr3=NULL;

	STFTObj stftObj=NULL;

	int *mTimeIndexArr=NULL;
	int *mFreIndexArr=NULL;

	int *mTempIndexArr=NULL;

	stftObj=reassignObj->stftObj;

	fftLength=reassignObj->fftLength;

	timeArr=reassignObj->timeArr;

	mReFreArr=reassignObj->mReFreArr;
	mReTimeArr=reassignObj->mReTimeArr;

	mRealArr1=reassignObj->mRealArr1;
	mImageArr1=reassignObj->mImageArr1;

	mRealArr2=reassignObj->mRealArr2;
	mImageArr2=reassignObj->mImageArr2;

	mRealArr3=reassignObj->mRealArr3;
	mImageArr3=reassignObj->mImageArr3;

	mTimeIndexArr=reassignObj->mTimeIndexArr;
	mFreIndexArr=reassignObj->mFreIndexArr;

	mTempIndexArr=reassignObj->mTempIndexArr;

	timeLength=stftObj_calTimeLength(stftObj,dataLength);
	if(reassignObj->timeLength<timeLength||
		reassignObj->timeLength>timeLength*2){
		free(mRealArr1);
		free(mImageArr1);

		free(mRealArr2);
		free(mImageArr2);

		free(mRealArr3);
		free(mImageArr3);

		free(timeArr);
		
		free(mReTimeArr);
		free(mReFreArr);

		free(mTimeIndexArr);
		free(mFreIndexArr);

		free(mTempIndexArr);

		mRealArr1=__vnew(timeLength*fftLength, NULL);
		mImageArr1=__vnew(timeLength*fftLength, NULL);

		mRealArr2=__vnew(timeLength*fftLength, NULL);
		mImageArr2=__vnew(timeLength*fftLength, NULL);

		mRealArr3=__vnew(timeLength*fftLength, NULL);
		mImageArr3=__vnew(timeLength*fftLength, NULL);

		mReTimeArr=__vnew(timeLength*(fftLength/2+1), NULL);
		mReFreArr=__vnew(timeLength*(fftLength/2+1), NULL);

		mTimeIndexArr=__vnewi(timeLength*(fftLength/2+1), NULL);
		mFreIndexArr=__vnewi(timeLength*(fftLength/2+1), NULL);

		mTempIndexArr=__vnewi(timeLength*(fftLength/2+1), NULL);

		__varange(0, timeLength, 1, &timeArr);
		for(int i=0;i<timeLength;i++){
			float _t=0;

			// isPadding True 和fftLength无关 False +fftLength/2 offset ???
			// _t=timeArr[i]*reassignObj->slideLength+(reassignObj->isPad?0:fftLength/2);
			_t=timeArr[i]*reassignObj->slideLength;
			timeArr[i]=_t/reassignObj->samplate;
		}
	}

	reassignObj->timeLength=timeLength;

	reassignObj->timeArr=timeArr;

	reassignObj->mReTimeArr=mReTimeArr;
	reassignObj->mReFreArr=mReFreArr;

	reassignObj->mRealArr1=mRealArr1;
	reassignObj->mImageArr1=mImageArr1;

	reassignObj->mRealArr2=mRealArr2;
	reassignObj->mImageArr2=mImageArr2;

	reassignObj->mRealArr3=mRealArr3;
	reassignObj->mImageArr3=mImageArr3;

	reassignObj->mTimeIndexArr=mTimeIndexArr;
	reassignObj->mFreIndexArr=mFreIndexArr;

	reassignObj->mTempIndexArr=mTempIndexArr;
}

static void _reassignObj_stft(ReassignObj reassignObj,float *dataArr,int dataLength){
	STFTObj stftObj=NULL;
	float *winArr=NULL; 

	int fftLength=0; 
	int timeLength=0;

	float *mRealArr1=NULL; // S_h
	float *mImageArr1=NULL;

	stftObj=reassignObj->stftObj;
	winArr=reassignObj->winArr;

	mRealArr1=reassignObj->mRealArr1;
	mImageArr1=reassignObj->mImageArr1;

	fftLength=reassignObj->fftLength;
	timeLength=reassignObj->timeLength;

	// reset windData & stft
	stftObj_useWindowDataArr(stftObj, winArr);
	stftObj_stft(stftObj, dataArr, dataLength, mRealArr1, mImageArr1);

	// timeLength*fftLength => timeLength*(fftLength/2+1) 
	__mccut(mRealArr1,mImageArr1,
			timeLength,fftLength,
			0,timeLength,
			0,fftLength/2+1,
			mRealArr1,mImageArr1);
}

/***
	w=w-Image(S_dh/S_h)
	t=t+Real(S_th/S_h)
****/
static void _reassignObj_reassignTimeFre(ReassignObj reassignObj,float *dataArr,int dataLength){
	ReassignType resType=Reassign_All;

	int samplate=0;
	STFTObj stftObj=NULL;

	int fftLength=0; 
	int timeLength=0;

	float *freArr=NULL;
	float *timeArr=NULL;

	float *mReFreArr=NULL;
	float *mReTimeArr=NULL;

	float *winDerivativeArr=NULL; // +1
	float *winWeightArr=NULL;

	float *mRealArr1=NULL; // S_h
	float *mImageArr1=NULL;

	float *mRealArr2=NULL; // S_dh
	float *mImageArr2=NULL;

	float *mRealArr3=NULL; // S_th
	float *mImageArr3=NULL;

	resType=reassignObj->resType;

	samplate=reassignObj->samplate;
	stftObj=reassignObj->stftObj;

	fftLength=reassignObj->fftLength;
	timeLength=reassignObj->timeLength;

	mRealArr1=reassignObj->mRealArr1;
	mImageArr1=reassignObj->mImageArr1;

	mRealArr2=reassignObj->mRealArr2;
	mImageArr2=reassignObj->mImageArr2;

	mRealArr3=reassignObj->mRealArr3;
	mImageArr3=reassignObj->mImageArr3;

	winDerivativeArr=reassignObj->winDerivativeArr;
	winWeightArr=reassignObj->winWeightArr;

	freArr=reassignObj->freArr;
	timeArr=reassignObj->timeArr;

	mReFreArr=reassignObj->mReFreArr;
	mReTimeArr=reassignObj->mReTimeArr;

	if(resType==Reassign_Fre||resType==Reassign_All){
		stftObj_useWindowDataArr(stftObj, winDerivativeArr+1); // +1
		stftObj_stft(stftObj, dataArr, dataLength, mRealArr2, mImageArr2);

		// timeLength*fftLength => timeLength*(fftLength/2+1) 
		__mccut(mRealArr2,mImageArr2,
				timeLength,fftLength,
				0,timeLength,
				0,fftLength/2+1,
				mRealArr2,mImageArr2);

	}

	if(resType==Reassign_Time||resType==Reassign_All){
		stftObj_useWindowDataArr(stftObj, winWeightArr);
		stftObj_stft(stftObj, dataArr, dataLength, mRealArr3, mImageArr3);

		// timeLength*fftLength => timeLength*(fftLength/2+1) 
		__mccut(mRealArr3,mImageArr3,
				timeLength,fftLength,
				0,timeLength,
				0,fftLength/2+1,
				mRealArr3,mImageArr3);
	}

	// mReFreArr w=w-image(S_dh/S_h)
	if(resType==Reassign_Fre||resType==Reassign_All){
		__mcdiv(mRealArr2,mImageArr2,
				mRealArr1,mImageArr1,
				timeLength,fftLength/2+1,
				mRealArr2,mImageArr2);

		__mmul_value(mImageArr2,-0.5*samplate/M_PI , timeLength, fftLength/2+1, mReFreArr);
		__madd_vector(mReFreArr, freArr,1, timeLength, fftLength/2+1, 1, NULL);
	}
	
	// mReTimeArr t=t+real(S_th/S_h)
	if(resType==Reassign_Time||resType==Reassign_All){
		__mcdiv(mRealArr3,mImageArr3,
				mRealArr1,mImageArr1,
				timeLength,fftLength/2+1,
				mRealArr3,mImageArr3);

		__mmul_value(mRealArr3, 1.0/samplate, timeLength, fftLength/2+1, mReTimeArr);
		__madd_vector(mReTimeArr, timeArr,0, timeLength, fftLength/2+1, 0, NULL);
	}

}

/***
	1 thresh & clip
	2. 默认值
****/
static void _reassignObj_filterTimeFre(ReassignObj reassignObj,int dataLength){
	int fftLength=0; 
	int timeLength=0;

	ReassignType resType;

	float *freArr=NULL;  // fftLength/2+1
	float *timeArr=NULL; // timeLength

	float *mReFreArr=NULL; // timeLength*(fftLength/2+1)
	float *mReTimeArr=NULL;

	float *mRealArr1=0; // S_h
	float *mImageArr1=0;

	int samplate=0;
	float thresh=0; // 0.001
	int mLen=0;

	float fmax=0;
	float tmax=0;

	samplate=reassignObj->samplate;
	thresh=reassignObj->thresh;
	resType=reassignObj->resType;

	fftLength=reassignObj->fftLength;
	timeLength=reassignObj->timeLength;

	freArr=reassignObj->freArr;
	timeArr=reassignObj->timeArr;

	mReFreArr=reassignObj->mReFreArr;
	mReTimeArr=reassignObj->mReTimeArr;

	mRealArr1=reassignObj->mRealArr1;
	mImageArr1=reassignObj->mImageArr1;

	mLen=fftLength/2+1;

	fmax=freArr[fftLength/2];
	tmax=timeArr[timeLength-1]; // ??? isPadding

	// debug
	// {
	// 	printf("mReFreArr is:\n");
	// 	__mdebug(mReFreArr, timeLength, fftLength/2+1, 1);
	// 	printf("\n");

	// 	printf("mReTimeArr is:\n");
	// 	__mdebug(mReTimeArr, timeLength, fftLength/2+1, 1);
	// 	printf("\n");
	// }

	// 1. thresh & clip 
	for(int i=0;i<timeLength;i++){
		for(int j=0;j<mLen;j++){
			float _power=0;
			float _r1=0;
			float _i1=0;

			float _value2=0;

			_r1=mRealArr1[i*mLen+j];
			_i1=mImageArr1[i*mLen+j];
			_power=_r1*_r1+_i1*_i1;

			if(resType==Reassign_Fre||resType==Reassign_All){ // fre
				// thresh 避免NaN
				if(_power>=thresh*thresh){
					_value2=mReFreArr[i*mLen+j];
				}
				else{
					_value2=freArr[j];
				}

				// clip
				if(_value2<0){
					_value2=0;
				}

				if(_value2>fmax){
					_value2=fmax;
				}

				mReFreArr[i*mLen+j]=_value2;
			}

			if(resType==Reassign_Time||resType==Reassign_All){ // time
				// thresh 避免NaN
				if(_power>=thresh*thresh){
					_value2=mReTimeArr[i*mLen+j];
				}
				else{
					_value2=timeArr[i];
				}

				// clip
				if(_value2<0){
					_value2=0;
				}

				if(_value2>tmax){
					_value2=tmax;
				}

				mReTimeArr[i*mLen+j]=_value2;
			}
		}
	}

	// 3. 默认值
	if(resType!=Reassign_All){
		if(resType!=Reassign_Fre){
			__mrepeat(freArr, 1, mLen, 0, timeLength, mReFreArr);
		}
		else if(resType!=Reassign_Time){
			__mrepeat(timeArr, timeLength, 1, 1, mLen, mReTimeArr);
		}
	}
}

void reassignObj_free(ReassignObj reassignObj){
	STFTObj stftObj=NULL; 

	float *freArr=NULL;  // fftLength/2+1
	float *timeArr=NULL; // timeLength

	float *mReFreArr=NULL; // timeLength*(fftLength/2+1)
	float *mReTimeArr=NULL;

	float *winArr=NULL; // S_h
	float *winDerivativeArr=NULL; // +1
	float *winWeightArr=NULL;

	// stft相关 timeLength*fftLength => timeLength*(fftLength/2+1)
	float *mRealArr1=NULL; // S_h
	float *mImageArr1=NULL;

	float *mRealArr2=NULL; // S_dh
	float *mImageArr2=NULL;

	float *mRealArr3=NULL; // S_th
	float *mImageArr3=NULL;

	int *mTimeIndexArr=NULL;
	int *mFreIndexArr=NULL;

	int *mTempIndexArr=NULL;

	if(!reassignObj){
		return;
	}

	stftObj=reassignObj->stftObj;

	freArr=reassignObj->freArr;
	timeArr=reassignObj->timeArr;

	mReFreArr=reassignObj->mReFreArr;
	mReTimeArr=reassignObj->mReTimeArr;

	winArr=reassignObj->winArr;
	winDerivativeArr=reassignObj->winDerivativeArr;
	winWeightArr=reassignObj->winWeightArr;

	mRealArr1=reassignObj->mRealArr1;
	mImageArr1=reassignObj->mImageArr1;

	mRealArr2=reassignObj->mRealArr2;
	mImageArr2=reassignObj->mImageArr2;

	mRealArr3=reassignObj->mRealArr3;
	mImageArr3=reassignObj->mImageArr3;

	mTimeIndexArr=reassignObj->mTimeIndexArr;
	mFreIndexArr=reassignObj->mFreIndexArr;

	mTempIndexArr=reassignObj->mTempIndexArr;

	stftObj_free(stftObj);

	free(freArr);
	free(timeArr);

	free(mReFreArr);
	free(mReTimeArr);

	free(winArr);
	free(winDerivativeArr);
	free(winWeightArr);

	free(mRealArr1);
	free(mImageArr1);

	free(mRealArr2);
	free(mImageArr2);

	free(mRealArr3);
	free(mImageArr3);

	free(mTimeIndexArr);
	free(mFreIndexArr);

	free(mTempIndexArr);

	free(reassignObj);
}





```

---

### Archivo: `./src/flux_temporal.h`

```


#ifndef FLUX_TEMPORAL_H
#define FLUX_TEMPORAL_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>





#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/bft_algorithm.h`

```


#ifndef BFT_ALGORITHM_H
#define BFT_ALGORITHM_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "flux_base.h"

typedef struct OpaqueBFT *BFTObj;

/***
	num>=2&&num<=2048
	samplate 32000
	binPerOctave 12 >=4&&<=48
	
	radix2Exp 12 
	WindowType "hann"
	slideLength 1024

	filterScaleType "linear"
	filterStyleType "slaney"
	filterNormalType "none"
	dataType "power"

	isReassign 0
	isTemporal 0
****/
int bftObj_new(BFTObj *bftObj,int num,int radix2Exp,
			int *samplate,float *lowFre,float *highFre,int *binPerOctave,
			WindowType *windowType,int *slideLength,
			SpectralFilterBankScaleType *filterScaleType,
			SpectralFilterBankStyleType *filterStyleType,
			SpectralFilterBankNormalType *filterNormalType,
			SpectralDataType *dataType,
			int *isReassign,
			int *isTemporal);

int bftObj_calTimeLength(BFTObj bftObj,int dataLength);

float *bftObj_getFreBandArr(BFTObj bftObj);
int *bftObj_getBinBandArr(BFTObj bftObj);

// 0 complex,1 real ->mRealArr
void bftObj_setResultType(BFTObj bftObj,int type);
void bftObj_setDataNormValue(BFTObj bftObj,float normValue);

void bftObj_bft(BFTObj bftObj,float *dataArr,int dataLength,float *mRealArr3,float *mImageArr3);

// energy/rms/zeroCrossRate
void bftObj_getTemporalData(BFTObj bftObj,float **eArr,float **rArr,float **zArr);

void bftObj_free(BFTObj bftObj);

#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/temporal_algorithm.h`

```


#ifndef TEMPORAL_ALGORITHM_H
#define TEMPORAL_ALGORITHM_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "flux_base.h"

typedef struct OpaqueTemporal *TemporalObj;

/***
	frameLength 2048
	slideLength 512
	windowType Hann
****/
int temporalObj_new(TemporalObj *temporalObj,
			 		int *frameLength,int *slideLength,WindowType *windowType);

int temporalObj_calTimeLength(TemporalObj temporalObj,int dataLength);

void temporalObj_temporal(TemporalObj temporalObj,float *dataArr,int dataLength);

/***
	energy/rms/zeroCrossRate
	mDataArr timeLength*frameLength
****/
void temporalObj_getData(TemporalObj temporalObj,
						float **eArr,float **rArr,float **zArr,
						float **mDataArr);

// gamma 1/10/20 song 0.5
void temporalObj_ezr(TemporalObj temporalObj,float gamma,float *vArr3);

void temporal_free(TemporalObj temporalObj);

#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/dsp/flux_correct.h`

```


#ifndef FLUX_CORRECT_H
#define FLUX_CORRECT_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

/***
	频谱校正:频率/幅值/相位 校正都是基于未恢复幅值进行的!!!
	rect/hann/hamm 三种基本窗的fre/amp校正以及amp恢复
	det 谱线修正量 
	value 幅值校正值
****/
void correct_rect(float cur,float left,float right,float *det,float *value);
void correct_hann(float cur,float left,float right,float *det,float *value);
void correct_hamm(float cur,float left,float right,float *det,float *value);

float correct_getRectRecover();
float correct_getHannRecover();
float correct_getHammRecover();

#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/dsp/flux_correct.c`

```
// 

#include <string.h>
#include <math.h>

#include "../vector/flux_vector.h"
#include "../vector/flux_vectorOp.h"

#include "flux_correct.h"

void correct_rect(float cur,float left,float right,float *det,float *value){
	float _det=0;
	float _value=0;

	double eps=1e-10;

	float y1=0;
	float y2=0;

	float v1=0;
	float v2=0;

	float n=0;
	float s=0;

	float c1=0;
	float c2=0;

	if(right>=left){
		y1=cur;
		y2=right;
	}
	else{
		y1=left;
		y2=cur;
	}

	if(y2<eps){
		y2=eps;
	}

	// 1. det计算
	v1=y1/y2;
	v2=1+v1;
	if(v2<eps){
		v2=eps;
	}

	_det=1/v2;
	if(y1<y2){
		_det-=1;
	}

	// 2. value计算
	if(_det>=0){
		n=floorf(_det);
	}
	else{
		n=ceilf(_det);
	}
	s=_det-n;
	
	if(fabs(s)<1e-8){
		s=1e-8;
	}

	c1=n+s;
	c2=M_PI*c1/sinf(M_PI*c1);

	_value=cur*c2;

	if(det){
		*det=_det;
	}

	if(value){
		*value=_value;
	}
}

void correct_hann(float cur,float left,float right,float *det,float *value){
	float _det=0;
	float _value=0;

	double eps=1e-10;

	float y1=0;
	float y2=0;

	float v1=0;
	float v2=0;

	float n=0;
	float s=0;

	float c1=0;
	float c2=0;

	if(right>=left){
		y1=cur;
		y2=right;
	}
	else{
		y1=left;
		y2=cur;
	}

	if(y2<eps){
		y2=eps;
	}

	// 1. det计算
	v1=y1/y2;
	v2=1+v1;
	if(v2<eps){
		v2=eps;
	}

	_det=(2-v1)/v2;
	if(y1<y2){
		_det-=1;
	}

	// 2. value计算
	if(_det>=0){
		n=floorf(_det);
	}
	else{
		n=ceilf(_det);
	}
	s=_det-n;
	
	if(fabs(s)<1e-8){
		s=1e-8;
	}

	c1=n+s;
	c2=M_PI*c1/sinf(M_PI*c1);

	_value=cur*c2*(1-c1*c1)*2;

	if(det){
		*det=_det;
	}

	if(value){
		*value=_value;
	}
}

void correct_hamm(float cur,float left,float right,float *det,float *value){
	float _det=0;
	float _value=0;

	double eps=1e-10;

	float y1=0;
	float y2=0;

	float v1=0;
	float v2=0;

	float n=0;
	float s=0;

	float c1=0;
	float c2=0;

	if(right>=left){
		y1=cur;
		y2=right;
	}
	else{
		y1=left;
		y2=cur;
	}

	if(y2<eps){
		y2=eps;
	}

	// 1. det计算
	c1=-27.0/4;
	v1=y1/y2;

	_det=-(2-v1)/(1+v1);
	for(int i=0;i<8;i++){
		v2=(_det*_det+c1)/((_det+1)*(_det+1)+c1);
		_det=(v1-2*v2)/(v1+v2);
	}
	_det=-_det;

	if(y1<y2){
		_det-=1;
	}

	// 2. value计算
	if(_det>=0){
		n=floorf(_det);
	}
	else{
		n=ceilf(_det);
	}
	s=_det-n;
	
	if(fabs(s)<1e-8){
		s=1e-8;
	}

	c1=n+s;
	c2=M_PI*c1/sinf(M_PI*c1);

	_value=cur*c2*(1-c1*c1)/(0.54-0.08*c1*c1);

	if(det){
		*det=_det;
	}

	if(value){
		*value=_value;
	}
}

float correct_getRectRecover(){

	return 1;
}

float correct_getHannRecover(){

	return 1/0.5;
}

float correct_getHammRecover(){

	return 1/0.54;
}











```

---

### Archivo: `./src/dsp/phase_vocoder.c`

```
// 

#include <string.h>
#include <math.h>
#include <stdlib.h>
#include <time.h>

#include "../vector/flux_vector.h"
#include "../vector/flux_vectorOp.h"
#include "../vector/flux_complex.h"

#include "phase_vocoder.h"

/***
	mDataArr1 stft time*fftLength
	rate 0.5~2
	slideLength fftLength/4
****/
void phase_vocoder(float *mRealArr1,float *mImageArr1,int nLength,int mLength,int slideLength,float rate,
				float *mRealArr2,float *mImageArr2){
	float *timeArr=NULL;
	float *phiArr=NULL;
	float *phaseArr=NULL;

	float *arr1=NULL;
	float *arr2=NULL;

	float *arr3=NULL;
	float *arr4=NULL;

	int tLen=0;
	int fLen=0;

	fLen=mLength/2+1;
	tLen=ceilf(nLength/rate);
	__varange(0,nLength,rate,&timeArr);

	phiArr=__vlinspace(0, M_PI*slideLength, fLen, 0);

	phaseArr=__vnew(fLen, NULL);
	__vcangle(mRealArr1,mImageArr1,fLen,phaseArr);

	arr1=__vnew(fLen, NULL);
	arr2=__vnew(fLen, NULL);

	arr3=__vnew(fLen, NULL);
	arr4=__vnew(fLen, NULL);
	for(int i=0;i<tLen;i++){
		int k=0;
		float alpha=0;

		float *rArr1=NULL;
		float *iArr1=NULL;

		float *rArr2=NULL;
		float *iArr2=NULL;

		k=floorf(timeArr[i]);
		alpha=timeArr[i]-floorf(timeArr[i]);

		if(k<nLength){
			rArr1=mRealArr1+k*mLength;
			iArr1=mImageArr1+k*mLength;
		}
		else{
			memset(arr1,0,sizeof(float )*fLen);
			memset(arr2,0,sizeof(float )*fLen);
			rArr1=arr1;
			iArr1=arr2;
		}
		
		if(k+1<nLength){
			rArr2=mRealArr1+(k+1)*mLength;
			iArr2=mImageArr1+(k+1)*mLength;
		}
		else{
			memset(arr3,0,sizeof(float )*fLen);
			memset(arr4,0,sizeof(float )*fLen);
			rArr2=arr3;
			iArr2=arr4;
		}

		__vcabs(rArr1, iArr1, fLen, arr1);
		__vcabs(rArr2, iArr2, fLen, arr2);
		__vmul_value(arr1, (1-alpha), fLen, NULL);
		__vmul_value(arr2, alpha, fLen, NULL);

		// cal data
		for(int j=0;j<fLen;j++){
			mRealArr2[i*mLength+j]=(arr1[j]+arr2[j])*cosf(phaseArr[j]);
			mImageArr2[i*mLength+j]=(arr1[j]+arr2[j])*sinf(phaseArr[j]);
		}

		for(int j=fLen,l=mLength/2-1;j<mLength;j++,l--){
			mRealArr2[i*mLength+j]=mRealArr2[i*mLength+l];
			mImageArr2[i*mLength+j]=-mImageArr2[i*mLength+l];
		}

		// update phase
		__vcangle(rArr2,iArr2,fLen,arr1);
		__vcangle(rArr1,iArr1,fLen,arr2);
		for(int j=0;j<fLen;j++){
			float value=0;

			value=arr1[j]-arr2[j]-phiArr[j];
			value=value-2*M_PI*roundf(value/(2*M_PI));

			phaseArr[j]+=(phiArr[j]+value);
		}
	}

	free(timeArr);
	free(phiArr);
	free(phaseArr);

	free(arr1);
	free(arr2);
	free(arr3);
	free(arr4);
}










```

---

### Archivo: `./src/dsp/flux_window.c`

```
// 

#include <string.h>
#include <math.h>

#include "../vector/flux_vector.h"

#include "flux_window.h"

static float *__calHalfHann(int halfLen,int length);
static float *__calHalfHamm(int halfLen,int length);
static float *__calHalfBlackman(int halfLen,int length);
static float *__calHalfFlattop(int halfLen,int length);

static float *__calHalfBartlett(int halfLen,int length);
static float *__calHalfTriang(int halfLen,int length);

static float __besselZeroOne(float value);
// alpha 默认5
static float *__calHalfKaiser(int halfLen,float alpha,int length);
// alpha 默认2.5
static float *__calHalfGauss(int halfLen,float alpha,int length);

static float *__calHalfBlackmanHarris(int halfLen,int length);
static float *__calHalfBlackmanNuttall(int halfLen,int length);
static float *__calHalfBartlettHann(int halfLen,int length);

static float *__calHalfBohman(int halfLen,int length);

static void __calKaiserOrder(float w1,float w2,float atten,int *order,float *beta);

static float *__window_createHann(int length,int flag);
static float *__window_createHamm(int length,int flag);

static float *__window_createBlackman(int length,int flag);
// beta 5.0
static float *__window_createKaiser(int length,float *beta);

// only symmetric
static float *__window_createBartlett(int length,int flag);
static float *__window_createTriang(int length,int flag);

static float *__window_createFlattop(int length,int flag);
// alpha 2.5
static float *__window_createGauss(int length,float *alpha);

// 4-term blackman harris~nuttall
static float *__window_createBlackmanHarris(int length,int flag);
static float *__window_createBlackmanNuttall(int length,int flag);
// like Bartlett,hann,hamm; only symmetric
static float *__window_createBartlettHann(int length,int flag);

// only symmetric
static float *__window_createBohman(int length,int flag);

// alpha>=0&&<=1 0.5 rect~hann ;only symmetric
static float *__window_createTukey(int length,float *alpha);

// order相关 
// w1 ws/wp w2 ws/wp atten dB
void window_calKaiserOrder(float w1,float w2,float atten,int *order,float *beta);

// 窗函数相关 flag 0 symmetric对称 1 periodic周期 针对fft length extend 1 sample
float *window_createHann(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createHann(flag?length+1:length,0);
		}
	}

	return arr;
}

float *window_createHamm(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createHamm(flag?length+1:length,0);
		}
	}

	return arr;
}


float *window_createBlackman(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createBlackman(flag?length+1:length,0);
		}
	}

	return arr;
}

// beta 5.0
float *window_createKaiser(int length,int flag,float *beta){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createKaiser(flag?length+1:length,beta);
		}
	}

	return arr;
}

// only symmetric
float *window_createBartlett(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createBartlett(flag?length+1:length,0);
		}
	}

	return arr;
}

float *window_createTriang(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createTriang(flag?length+1:length,0);
		}
	}

	return arr;
}

float *window_createFlattop(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createFlattop(flag?length+1:length,0);
		}
	}

	return arr;
}

// alpha 2.5
float *window_createGauss(int length,int flag,float *alpha){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createGauss(flag?length+1:length,alpha);
		}
	}

	return arr;
}


// 4-term blackman harris~nuttall
float *window_createBlackmanHarris(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createBlackmanHarris(flag?length+1:length,0);
		}
	}

	return arr;
}

float *window_createBlackmanNuttall(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createBlackmanNuttall(flag?length+1:length,0);
		}
	}

	return arr;
}

// like Bartlett,hann,hamm; only symmetric
float *window_createBartlettHann(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createBartlettHann(flag?length+1:length,0);
		}
	}

	return arr;
}

// only symmetric
float *window_createBohman(int length,int flag){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createBohman(flag?length+1:length,0);
		}
	}

	return arr;
}

// alpha>=0&&<=1 0.5 rect~hann ;only symmetric
float *window_createTukey(int length,int flag,float *alpha){
	float *arr=NULL;

	if(length>0){
		if(length==1){
			arr=__vnew(1, NULL);
			arr[0]=1;
		}
		else{
			arr=__window_createTukey(flag?length+1:length,alpha);
		}
	}

	return arr;
}

static float *__window_createHann(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<1){
		return NULL;
	}
	
	if(!(length&1)){ // even
		halfLen=length/2+flag; // 针对periodic +1
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfHann(halfLen,length-1+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createHamm(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<1){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag; // 针对periodic +1
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfHamm(halfLen,length-1+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createBlackman(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<1){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag; // 针对periodic +1
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfBlackman(halfLen,length-1+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createBlackmanHarris(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<1){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfBlackmanHarris(halfLen,length-1+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createBlackmanNuttall(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<1){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfBlackmanNuttall(halfLen,length-1+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createKaiser(int length,float *alpha){
	float *wArr=NULL;
	int halfLen=0;

	float a=5.0;

	if(length<2){
		return NULL;
	}

	if(alpha){
		if(*alpha>0){
			a=*alpha;
		}
	}

	if(!(length&1)){ // even
		halfLen=length/2;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfKaiser(halfLen,a,length-1);
	for(int i=length-1,j=0;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

// bartlett/triang 三角窗相关 length=N+1 !!!
static float *__window_createBartlett(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<2){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfBartlett(halfLen,length-1+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createBartlettHann(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<2){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfBartlettHann(halfLen,length-1+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createTriang(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<1){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfTriang(halfLen,length+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createFlattop(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<1){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfFlattop(halfLen,length-1+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createGauss(int length,float *alpha){
	float *wArr=NULL;
	int halfLen=0;

	float a=2.5;

	if(length<2){
		return NULL;
	}

	if(alpha){
		if(*alpha>0){
			a=*alpha;
		}
	}

	if(!(length&1)){ // even
		halfLen=length/2+1;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfGauss(halfLen,a,length);
	for(int i=length-1,j=0;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createBohman(int length,int flag){
	float *wArr=NULL;
	int halfLen=0;

	if(length<1){
		return NULL;
	}

	if(!(length&1)){ // even
		halfLen=length/2+flag;
	}
	else{ // odd
		halfLen=(length+1)/2;
	}

	wArr=__calHalfBohman(halfLen,length+flag);
	for(int i=length-1,j=flag;i>=halfLen;i--,j++){
		wArr[i]=wArr[j];
	}

	return wArr;
}

static float *__window_createTukey(int length,float *alpha){
	float *wArr=NULL;
	float *xArr=NULL;

	float a=0.5;

	if(alpha){
		if(*alpha>=0&&*alpha<=1){
			a=*alpha;
		}
	}

	if(a==0){ // rect
		float _v=1;

		wArr=__vnew(length, &_v);
		return wArr;
	}
	else if(a==1){ // hann
		wArr=window_createHann(length, 0); // symmetric
		return wArr;
	}

	wArr=__vnew(length, NULL);
	xArr=__vlinspace(0, 1, length, 0);
	for(int i=0;i<length;i++){
		float _x=0;

		_x=xArr[i];
		if(_x>=0&&_x<a/2){
			wArr[i]=0.5*(1+cosf(2*M_PI/a*(_x-a/2)));
		}
		else if(_x>=a/2&&_x<(1-a/2)){
			wArr[i]=1;
		}
		else{ // 1-r/2~1
			wArr[i]=0.5*(1+cosf(2*M_PI/a*(_x-1+a/2)));
		}
	}

	free(xArr);
	return wArr;
}

static float *__calHalfBartlett(int halfLen,int length){
	float *arr=NULL;

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=0;i<halfLen;i++){
		arr[i]=2.0*i/length;
	}

	return arr;
}

// i=1 start
static float *__calHalfBartlettHann(int halfLen,int length){
	float *arr=NULL;

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=1;i<halfLen;i++){
		arr[i]=0.62-0.48*fabs(1.0*i/length-0.5)+0.38*cosf(2*M_PI*(1.0*i/length-0.5));
	}

	return arr;
}

static float *__calHalfTriang(int halfLen,int length){
	float *arr=NULL;

	int len=0;
	float det=0;

	if(!(length&1)){ // even
		det=0.5;
	}
	else{ // odd
		det=1;
		len=1;
	}

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=0;i<=halfLen;i++){
		arr[i]=2.0*(i+det)/(length+len);
	}

	return arr;
}

/****
	I(a)为零阶第一类修正贝塞尔函数
	I(a)=1+累加(k=1,无情大)[(1/k!(a/2)^k)^2]
	a一般取4~9,可以更小
****/
static float __besselZeroOne(float a){
	float sum=0;
	float b=0;

	float num=0;
	float den=0;
	float mid=0;

	sum=1;
	b=a/2;
	num=1;
	den=1;

	for(int k=1;k<16;k++){ // 一般取15~25 8即可满足精度
		num=num*b;
		den=den*k;
		mid=num/den;
		sum=sum+mid*mid;
	}

	return sum;
}

/***
	w(n)=I(b)/I(a) n>=0&&n<N-1;
	b=sqrt(1-(2*n/(N-1)-1)^2);
	a一般取4~9,可以更小
****/
static float *__calHalfKaiser(int halfLen,float a,int length){
	float *arr=NULL;

	float num=0;
	float den=0;
	float b=0;

	arr=__vnew(halfLen*2+1, NULL);
	den=__besselZeroOne(a);
	for(int i=0;i<halfLen;i++){
		float _value=0;

		_value=2.0*i/length-1;
		b=a*sqrtf(1-_value*_value);
		num=__besselZeroOne(b);
		arr[i]=num/den;
	}

	return arr;
}

// gauss函数
static float *__calHalfGauss(int halfLen,float a,int length){
	float *arr=NULL;
	float det=0;

	if(!(length&1)){ // even
		det=0.5;
	}

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=halfLen-1,j=0;i>=0;i--,j++){
		float _value=0;

		_value=2*a*(i-det)/(length-1);
		_value=-0.5*_value*_value;
		arr[j]=expf(_value);
	}

	return arr;
}

static float *__calHalfHann(int halfLen,int length){
	float *arr=NULL;

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=0;i<halfLen;i++){
		arr[i]=0.5-0.5*cosf(2*M_PI*i/length);
	}

	return arr;
}

static float *__calHalfHamm(int halfLen,int length){
	float *arr=NULL;

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=0;i<halfLen;i++){
		arr[i]=0.54-0.46*cosf(2*M_PI*i/length);
	}

	return arr;
}

// i=1 start
static float *__calHalfBlackman(int halfLen,int length){
	float *arr=NULL;

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=1;i<halfLen;i++){
		arr[i]=0.42-0.5*cosf(2*M_PI*i/length)+0.08*cosf(4*M_PI*i/length);
	}

	return arr;
}

// i=1 start
static float *__calHalfBohman(int halfLen,int length){
	float *arr=NULL;
	float *lArr=NULL;

	arr=__vnew(halfLen*2+1, NULL);
	lArr=__vlinspace(-1, 1, length, 0);
	for(int i=1;i<halfLen;i++){
		arr[i]=(1-fabsf(lArr[i]))*cosf(M_PI*fabsf(lArr[i]))+1/M_PI*sinf(M_PI*fabsf(lArr[i]));
	}

	free(lArr);
	return arr;
}

static float *__calHalfBlackmanHarris(int halfLen,int length){
	float *arr=NULL;

	float a0=0;
	float a1=0;
	float a2=0;
	float a3=0;

	a0=0.35875;
	a1=0.48829;
	a2=0.14128;
	a3=0.01168;

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=0;i<halfLen;i++){
		arr[i]=a0-a1*cosf(2*M_PI*i/length)+
				a2*cosf(4*M_PI*i/length)-
				a3*cosf(6*M_PI*i/length);
	}

	return arr;
}

static float *__calHalfBlackmanNuttall(int halfLen,int length){
	float *arr=NULL;

	float a0=0;
	float a1=0;
	float a2=0;
	float a3=0;

	a0=0.3635819;
	a1=0.4891775;
	a2=0.1365995;
	a3=0.0106411;

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=0;i<halfLen;i++){
		arr[i]=a0-a1*cosf(2*M_PI*i/length)+
				a2*cosf(4*M_PI*i/length)-
				a3*cosf(6*M_PI*i/length);
	}

	return arr;
}

static float *__calHalfFlattop(int halfLen,int length){
	float *arr=NULL;

	float a0=0;
	float a1=0;
	float a2=0;
	float a3=0;
	float a4=0;

	a0=0.21557895;
	a1=0.41663158;
	a2=0.277263158;
	a3=0.083578947;
	a4=0.006947368;

	arr=__vnew(halfLen*2+1, NULL);
	for(int i=0;i<halfLen;i++){
		arr[i]=a0-a1*cosf(2*M_PI*i/length)+
				a2*cosf(4*M_PI*i/length)-
				a3*cosf(6*M_PI*i/length)+
				a4*cosf(8*M_PI*i/length);
	}

	return arr;
}

void window_calKaiserOrder(float w1,float w2,float atten,int *order,float *beta){

	__calKaiserOrder(w1,w2,atten,order,beta);
}

static void __calKaiserOrder(float w1,float w2,float atten,int *order,float *beta){
	int _order=0;
	float _beta=0;

	if(w1<=0||w1>=1||w2<=0||w2>=1){
		return;
	}

	_order=ceilf((atten-7.95)/(M_PI*2.285*fabsf(w1-w2)));
	if(atten>50){
		_beta=0.1102*(atten-8.7);
	}
	else if(atten>=21){
		_beta=0.5842*powf((atten-21), 0.4)+
    			0.07886*(atten-21);
	}

	if(order){
		*order=_order;
	}

	if(beta){
		*beta=_beta;
	}
}

float *window_calFFTWindow(WindowType winType,int length){
	float *dataArr=NULL;

	if(winType==Window_Hann){
		dataArr=window_createHann(length,1);
	}
	else if(winType==Window_Hamm){
		dataArr=window_createHamm(length,1);
	}
	else if(winType==Window_Blackman){
		dataArr=window_createBlackman(length,1);
	}
	else if(winType==Window_Kaiser){ // beta 5
		dataArr=window_createKaiser(length,1,NULL);
	}
	else if(winType==Window_Bartlett){ // symmetric
		dataArr=window_createBartlett(length,0);
	}
	else if(winType==Window_Triang){ // symmetric
		dataArr=window_createTriang(length,0);
	}
	else if(winType==Window_Flattop){
		dataArr=window_createFlattop(length,1);
	}
	else if(winType==Window_Gauss){ // alpha 2.5
		dataArr=window_createGauss(length,1,NULL);
	}
	else if(winType==Window_Blackman_Harris){
		dataArr=window_createBlackmanHarris(length,1);
	}
	else if(winType==Window_Blackman_Nuttall){
		dataArr=window_createBlackmanNuttall(length,1);
	}
	else if(winType==Window_Bartlett_Hann){ // symmetric
		dataArr=window_createBartlettHann(length,0);
	}
	else if(winType==Window_Bohman){ // symmetric
		dataArr=window_createBohman(length,0);
	}
	else if(winType==Window_Tukey){ // alpha 0.5
		dataArr=window_createTukey(length,1,NULL);
	}
	else { // rect
		dataArr=(float *)calloc(length, sizeof(float ));
		for(int i=0;i<length;i++){
			dataArr[i]=1;
		}
	}

	return dataArr;
}























```

---

### Archivo: `./src/dsp/fft_algorithm.c`

```
// clang -g -c fft_algorithm.c -o fft.o && ar -r libfft.a fft.o

#include <string.h>
#include <math.h>

#ifdef HAVE_ACCELERATE
#include <Accelerate/Accelerate.h>

#elif defined HAVE_FFTW3F
#include <fftw3.h>
#include <pthread.h>

#elif defined HAVE_MKL
#include <mkl.h>
#include <mkl_dfti.h>

#endif

#include "fft_algorithm.h"

typedef enum{
	FFTExec_None=0,

	FFTExec_FFT,
	FFTExec_IFFT,

	FFTExec_DCT,
	FFTExec_IDCT,

} FFTExecType;

struct OpaqueFFT{
	FFTExecType execType;

	int radix2Exp; // 2 power
	int fftLength; // length
	int wLength; // w length; fftLength/2

	float s0; // dct scale coef
	float s1;

	int *indexArr; // reverse order cache

	float *wCosArr; // fft w cache
	float *wSinArr;

	float *wCosArr1; // dct w cache; fftLength
	float *wSinArr1;

	float *realArr1; // fft input r,i cache
	float *imageArr1;

	float *realArr2; // fft output r,i cache
	float *imageArr2;

	int rFlag; // real flag

	#ifdef HAVE_ACCELERATE
	FFTSetup setup;

	DSPSplitComplex inData;
	DSPSplitComplex outData;

	#elif defined HAVE_FFTW3F
	fftwf_plan planReal; // real
	fftwf_plan planComplex; // complex
	fftwf_plan planInverse; // inverse

	float *inData1;
	fftwf_complex *outData1;

	fftwf_complex *inData2;
	fftwf_complex *outData2;

	fftwf_complex *inData3;
	fftwf_complex *outData3;

	#elif defined HAVE_MKL
	DFTI_DESCRIPTOR_HANDLE handleReal; // real
	DFTI_DESCRIPTOR_HANDLE handleComplex; // complex
	DFTI_DESCRIPTOR_HANDLE handleInverse; // inverse

	float *outData1;

	MKL_Complex8 *inData2;
	MKL_Complex8 *outData2;

	MKL_Complex8 *inData3;
	MKL_Complex8 *outData3;

	#endif
};

static int *_createIndexArr(int n,int length);

static void _createWArr(float *wCosArr,float *wSinArr,int wLength);
static void _createWArr1(float *wCosArr,float *wSinArr,int wLength);

static void _vmulReal(float *realArr,float *imageArr,float *wCosArr,float *wSinArr,int length);

static void _fftObj_init(FFTObj fftObj);

// flag 0 forward 1 backward
static void _fftObj_fft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2,int flag);

int fftObj_new(FFTObj *fftObj,int radix2Exp){
	int status=0;
	FFTObj fft=NULL;

	int length=0;
	int wLength=0;

	float s0=0;
	float s1=0;

	float *realArr1=NULL;
	float *imageArr1=NULL;

	float *realArr2=NULL;
	float *imageArr2=NULL;

	// int *indexArr=NULL; // reverse order cache
	// float *wCosArr=NULL; // fft w cache
	// float *wSinArr=NULL;

	// float *wCosArr1=NULL; // dct w cache; length
	// float *wSinArr1=NULL;

	if(radix2Exp<1||radix2Exp>30){
		status=-100;
		return status;
	}

	fft=*fftObj=(FFTObj )calloc(1, sizeof(struct OpaqueFFT ));

	length=1<<radix2Exp;
	wLength=1<<(radix2Exp-1);

	s0=sqrtf(1.0/length);
	s1=sqrtf(2.0/length);

	realArr1=(float *)calloc(length, sizeof(float ));
	imageArr1=(float *)calloc(length,sizeof(float ));

	realArr2=(float *)calloc(length, sizeof(float ));
	imageArr2=(float *)calloc(length,sizeof(float ));

	// reverse order cache
	// indexArr=_createIndexArr(radix2Exp, length);

	// // w cache
	// wCosArr=(float *)calloc(wLength, sizeof(float ));
	// wSinArr=(float *)calloc(wLength, sizeof(float ));
	// _createWArr(wCosArr, wSinArr, wLength);

	// wCosArr1=(float *)calloc(length, sizeof(float ));
	// wSinArr1=(float *)calloc(length, sizeof(float ));
	// _createWArr1(wCosArr1, wSinArr1, length);

	fft->radix2Exp=radix2Exp;
	fft->fftLength=length;
	fft->wLength=wLength;

	fft->s0=s0;
	fft->s1=s1;

	fft->realArr1=realArr1;
	fft->imageArr1=imageArr1;

	fft->realArr2=realArr2;
	fft->imageArr2=imageArr2;

	// fft->indexArr=indexArr;
	
	// fft->wCosArr=wCosArr;
	// fft->wSinArr=wSinArr;

	// fft->wCosArr1=wCosArr1;
	// fft->wSinArr1=wSinArr1;

	// _fftObj_init(fft);

	return status;
}

static void _fftObj_init(FFTObj fftObj){
	int radix2Exp=0; // 2 power
	int fftLength=0;

	radix2Exp=fftObj->radix2Exp;
	fftLength=fftObj->fftLength;

	#ifdef HAVE_ACCELERATE
	fftObj->setup=vDSP_create_fftsetup(radix2Exp,FFT_RADIX2);

	#elif defined HAVE_FFTW3F
	fftObj->inData1=(float *)fftwf_malloc(fftLength*sizeof(float ));
	fftObj->outData1=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));

	fftObj->planReal=fftwf_plan_dft_r2c_1d(fftLength,
												fftObj->inData1,fftObj->outData1,
												FFTW_ESTIMATE);

	fftObj->inData2=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));
	fftObj->outData2=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));

	fftObj->planComplex=fftwf_plan_dft_1d(fftLength,
										fftObj->inData2,fftObj->outData2,
										FFTW_FORWARD,FFTW_ESTIMATE);

	fftObj->inData3=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));
	fftObj->outData3=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));

	fftObj->planInverse=fftwf_plan_dft_1d(fftLength,
										fftObj->inData3,fftObj->outData3,
										FFTW_BACKWARD,FFTW_ESTIMATE);

	#elif defined HAVE_MKL
	DftiCreateDescriptor(&fftObj->handleReal, DFTI_SINGLE, DFTI_REAL, 1, fftLength);
	DftiSetValue(fftObj->handleReal, DFTI_PLACEMENT, DFTI_NOT_INPLACE);
	DftiCommitDescriptor(fftObj->handleReal);

	fftObj->outData1=(float *)calloc(fftLength+2, sizeof(float ));

	DftiCreateDescriptor(&fftObj->handleComplex, DFTI_SINGLE, DFTI_COMPLEX, 1, fftLength);
	DftiSetValue(fftObj->handleComplex, DFTI_PLACEMENT, DFTI_NOT_INPLACE);
	DftiCommitDescriptor(fftObj->handleComplex);

	fftObj->inData2=(MKL_Complex8 *)mkl_calloc(fftLength,sizeof(MKL_Complex8 ),64);
	fftObj->outData2=(MKL_Complex8 *)mkl_calloc(fftLength,sizeof(MKL_Complex8 ),64);

	DftiCreateDescriptor(&fftObj->handleInverse, DFTI_SINGLE, DFTI_COMPLEX, 1, fftLength);
	DftiSetValue(fftObj->handleInverse, DFTI_PLACEMENT, DFTI_NOT_INPLACE);
	DftiSetValue(fftObj->handleInverse, DFTI_BACKWARD_SCALE, 1.0/fftLength);
	DftiCommitDescriptor(fftObj->handleInverse);

	fftObj->inData3=(MKL_Complex8 *)mkl_calloc(fftLength,sizeof(MKL_Complex8 ),64);
	fftObj->outData3=(MKL_Complex8 *)mkl_calloc(fftLength,sizeof(MKL_Complex8 ),64);

	#endif
	
}

#ifdef HAVE_ACCELERATE
static void _fftObj_fft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2,int flag){
	int radix2Exp=0;
	int fftLength=0;

	int rFlag=0;

	radix2Exp=fftObj->radix2Exp;
	fftLength=fftObj->fftLength;

	rFlag=fftObj->rFlag;

	if(!fftObj->setup){
		fftObj->setup=vDSP_create_fftsetup(radix2Exp,FFT_RADIX2);
	}

	fftObj->inData.realp=realArr1;
	fftObj->inData.imagp=imageArr1;

	fftObj->outData.realp=realArr2;
	fftObj->outData.imagp=imageArr2;

	// if(rFlag){ // real to complex fft has problem !!!
	// 	vDSP_fft_zrop(fftObj->setup,
	// 				&fftObj->inData,1,&fftObj->outData,1,
	// 				radix2Exp,FFT_FORWARD);
	// }
	// else{
	// 	vDSP_fft_zop(fftObj->setup,
	// 				&fftObj->inData,1,&fftObj->outData,1,
	// 				radix2Exp,FFT_FORWARD);
	// }

	vDSP_fft_zop(fftObj->setup,
				&fftObj->inData,1,&fftObj->outData,1,
				radix2Exp,flag?FFT_INVERSE:FFT_FORWARD);

}

#elif defined HAVE_FFTW3F
static void _fftObj_fft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2,int flag){
	int radix2Exp=0;
	int fftLength=0;

	int rFlag=0;

	radix2Exp=fftObj->radix2Exp;
	fftLength=fftObj->fftLength;

	rFlag=fftObj->rFlag;

	if(rFlag&&!flag){ // real&&forward
		if(!fftObj->planReal){
			fftObj->inData1=(float *)fftwf_malloc(fftLength*sizeof(float ));
			fftObj->outData1=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));

			fftObj->planReal=fftwf_plan_dft_r2c_1d(fftLength,
												fftObj->inData1,fftObj->outData1,
												FFTW_ESTIMATE);
		}

		memcpy(fftObj->inData1, realArr1, sizeof(float )*fftLength);

		fftwf_execute(fftObj->planReal);

		for(int i=0;i<=fftLength/2;i++){
			realArr2[i]=fftObj->outData1[i][0];
			imageArr2[i]=fftObj->outData1[i][1];
		}

		for(int i=fftLength/2+1,j=fftLength/2-1;i<fftLength;i++,j--){
			realArr2[i]=realArr2[j];
			imageArr2[i]=-imageArr2[j];
		}
	}
	else{ // complex
		if(!flag){ // forward
			if(!fftObj->planComplex){
				fftObj->inData2=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));
				fftObj->outData2=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));

				fftObj->planComplex=fftwf_plan_dft_1d(fftLength,
													fftObj->inData2,fftObj->outData2,
													FFTW_FORWARD,FFTW_ESTIMATE);
			}

			for(int i=0;i<fftLength;i++){
				fftObj->inData2[i][0]=realArr1[i];
				fftObj->inData2[i][1]=imageArr1[i];
			}

			fftwf_execute(fftObj->planComplex);

			for(int i=0;i<fftLength;i++){
				realArr2[i]=fftObj->outData2[i][0];
				imageArr2[i]=fftObj->outData2[i][1];
			}
		}
		else{ // inverse
			if(!fftObj->planInverse){
				fftObj->inData3=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));
				fftObj->outData3=(fftwf_complex *)fftwf_malloc(fftLength*sizeof(fftwf_complex ));

				fftObj->planInverse=fftwf_plan_dft_1d(fftLength,
													fftObj->inData3,fftObj->outData3,
													FFTW_BACKWARD,FFTW_ESTIMATE);
			}

			for(int i=0;i<fftLength;i++){
				fftObj->inData3[i][0]=realArr1[i];
				fftObj->inData3[i][1]=imageArr1[i];
			}

			fftwf_execute(fftObj->planInverse);

			for(int i=0;i<fftLength;i++){
				realArr2[i]=fftObj->outData3[i][0];
				imageArr2[i]=fftObj->outData3[i][1];
			}
		}
	}
}

#elif defined HAVE_MKL
static void _fftObj_fft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2,int flag){
	int radix2Exp=0;
	int fftLength=0;

	int rFlag=0;

	radix2Exp=fftObj->radix2Exp;
	fftLength=fftObj->fftLength;

	rFlag=fftObj->rFlag;

	if(rFlag&&!flag){ // real&&forward
		if(!fftObj->handleReal){
			DftiCreateDescriptor(&fftObj->handleReal, DFTI_SINGLE, DFTI_REAL, 1, fftLength);
			DftiSetValue(fftObj->handleReal, DFTI_PLACEMENT, DFTI_NOT_INPLACE);
			DftiCommitDescriptor(fftObj->handleReal);

			fftObj->outData1=(float *)calloc(fftLength+2, sizeof(float ));
		}

		DftiComputeForward(fftObj->handleReal, realArr1, fftObj->outData1);

		for(int i=0;i<fftLength/2+1;i++){
			realArr2[i]=fftObj->outData1[2*i];
			imageArr2[i]=fftObj->outData1[2*i+1];
		}

		for(int i=fftLength/2+1;i<fftLength;i++){
		    realArr2[i]=realArr2[fftLength-i];
		    imageArr2[i]=-imageArr2[fftLength-i];
		}
	}
	else{ // complex
		if(!flag){ // forward
			if(!fftObj->handleComplex){
				DftiCreateDescriptor(&fftObj->handleComplex, DFTI_SINGLE, DFTI_COMPLEX, 1, fftLength);
				DftiSetValue(fftObj->handleComplex, DFTI_PLACEMENT, DFTI_NOT_INPLACE);
				DftiCommitDescriptor(fftObj->handleComplex);

				fftObj->inData2=(MKL_Complex8 *)mkl_calloc(fftLength,sizeof(MKL_Complex8 ),64);
				fftObj->outData2=(MKL_Complex8 *)mkl_calloc(fftLength,sizeof(MKL_Complex8 ),64);
			}

			for(int i=0;i<fftLength;i++){
				fftObj->inData2[i].real=realArr1[i];
				fftObj->inData2[i].imag=imageArr1[i];
			}

			DftiComputeForward(fftObj->handleComplex, fftObj->inData2, fftObj->outData2);

			for(int i=0;i<fftLength;i++){
				realArr2[i]=fftObj->outData2[i].real;
				imageArr2[i]=fftObj->outData2[i].imag;
			}
		}
		else{ // inverse
			if(!fftObj->handleInverse){
				DftiCreateDescriptor(&fftObj->handleInverse, DFTI_SINGLE, DFTI_COMPLEX, 1, fftLength);
				DftiSetValue(fftObj->handleInverse, DFTI_PLACEMENT, DFTI_NOT_INPLACE);
				DftiSetValue(fftObj->handleInverse, DFTI_BACKWARD_SCALE, 1.0/fftLength);
				DftiCommitDescriptor(fftObj->handleInverse);

				fftObj->inData3=(MKL_Complex8 *)mkl_calloc(fftLength,sizeof(MKL_Complex8 ),64);
				fftObj->outData3=(MKL_Complex8 *)mkl_calloc(fftLength,sizeof(MKL_Complex8 ),64);
			}

			for(int i=0;i<fftLength;i++){
				fftObj->inData3[i].real=realArr1[i];
				fftObj->inData3[i].imag=imageArr1[i];
			}

			DftiComputeBackward(fftObj->handleInverse, fftObj->inData3, fftObj->outData3);

			for(int i=0;i<fftLength;i++){
				realArr2[i]=fftObj->outData3[i].real;
				imageArr2[i]=fftObj->outData3[i].imag;
			}
		}
	}
}

#else
static void _fftObj_fft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2,int flag){
	int radix2Exp=0;
	int length=0;
	int wLength=0;

	int *indexArr=NULL; // reverse order cache

	float *wCosArr=NULL; // w cache
	float *wSinArr=NULL;

	int p=0; // 2 power
	int s=0; // step
	int w=0; // w
	int g=0; // group
	int b=0; // butterfly

	float wCos=0;
	float wSin=0;

	float tReal=0;
	float tImage=0;

	radix2Exp=fftObj->radix2Exp;
	length=fftObj->fftLength;
	wLength=fftObj->wLength;

	if(!fftObj->indexArr){
		// reverse order cache
		fftObj->indexArr=_createIndexArr(radix2Exp, length);

		// w cache
		fftObj->wCosArr=(float *)calloc(wLength, sizeof(float ));
		fftObj->wSinArr=(float *)calloc(wLength, sizeof(float ));
		_createWArr(fftObj->wCosArr, fftObj->wSinArr, wLength);
	}

	indexArr=fftObj->indexArr;

	wCosArr=fftObj->wCosArr;
	wSinArr=fftObj->wSinArr;

	// reverse
	for(int i=0;i<length;i++){
		realArr2[i]=realArr1[indexArr[i]];
		imageArr2[i]=imageArr1[indexArr[i]];
	}

	// butterfly algorithm
	for(p=1;p<=radix2Exp;p++){
		s=1<<(p-1);

		for(g=0;g<=s-1;g++){
			w=g*(1<<(radix2Exp-p));
			wCos=wCosArr[w];
			wSin=wSinArr[w];

			for(b=g;b<=length-1;b=b+(1<<p)){
				tReal=realArr2[b+s]*wCos-imageArr2[b+s]*wSin;
				tImage=realArr2[b+s]*wSin+imageArr2[b+s]*wCos;

				realArr2[b+s]=realArr2[b]-tReal;
				imageArr2[b+s]=imageArr2[b]-tImage;

				realArr2[b]=realArr2[b]+tReal;
				imageArr2[b]=imageArr2[b]+tImage;

			}
		}
	}
}

#endif

void fftObj_fft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2){
	int length=0;

	float *_realArr1=NULL;
	float *_imageArr1=NULL;

	length=fftObj->fftLength;

	_realArr1=fftObj->realArr1;
	_imageArr1=fftObj->imageArr1;

	if(realArr1&&!imageArr1){
		fftObj->rFlag=1;
	}

	// ???
	if(realArr1){
		memcpy(_realArr1, realArr1, sizeof(float )*length);
	}
	else{
		memset(_realArr1, 0, sizeof(float )*length);
	}

	if(imageArr1){
		memcpy(_imageArr1, imageArr1, sizeof(float )*length);
	}
	else{
		memset(_imageArr1, 0, sizeof(float )*length);
	}

	_fftObj_fft(fftObj,_realArr1,_imageArr1,realArr2,imageArr2,0);

	fftObj->execType=FFTExec_FFT;
	fftObj->rFlag=0;
}

void fftObj_ifft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2){
	int length=0;

	float *_realArr1=NULL;
	float *_imageArr1=NULL;

	length=fftObj->fftLength;

	_realArr1=fftObj->realArr1;
	_imageArr1=fftObj->imageArr1;

	// if(realArr1&&!imageArr1){
	// 	fftObj->rFlag=1;
	// }

	// ???
	if(realArr1){
		memcpy(_realArr1, realArr1, sizeof(float )*length);
	}
	else{
		memset(_realArr1, 0, sizeof(float )*length);
	}

	if(imageArr1){
		memcpy(_imageArr1, imageArr1, sizeof(float )*length);
	}
	else{
		memset(_imageArr1, 0, sizeof(float )*length);
	}

	// #ifdef HAVE_ACCELERATE
	// _fftObj_fft(fftObj,_realArr1,_imageArr1,realArr2,imageArr2,1);

	// #elif defined HAVE_FFTW3F
	// _fftObj_fft(fftObj,_realArr1,_imageArr1,realArr2,imageArr2,1);

	// #else

	// for(int i=0;i<length;i++){
	// 	_imageArr1[i]=-_imageArr1[i];
	// }

	// _fftObj_fft(fftObj,_realArr1,_imageArr1,realArr2,imageArr2,1);

	// for(int i=0;i<length;i++){
	// 	realArr2[i]=realArr2[i]/length;
	// 	imageArr2[i]=-imageArr2[i]/length;
	// }

	// #endif

	for(int i=0;i<length;i++){
		_imageArr1[i]=-_imageArr1[i];
	}

	_fftObj_fft(fftObj,_realArr1,_imageArr1,realArr2,imageArr2,0);

	for(int i=0;i<length;i++){
		realArr2[i]=realArr2[i]/length;
		imageArr2[i]=-imageArr2[i]/length;
	}

	fftObj->execType=FFTExec_IFFT;
	fftObj->rFlag=0;
}

void fftObj_dct(FFTObj fftObj,float *dataArr1,float *dataArr2,int isNorm){
	int length=0;

	float *wCosArr1=NULL;
	float *wSinArr1=NULL;

	float *_realArr1=NULL;
	float *_imageArr1=NULL;

	float *_realArr2=NULL;
	float *_imageArr2=NULL;

	length=fftObj->fftLength;

	if(!fftObj->wCosArr1){
		fftObj->wCosArr1=(float *)calloc(length, sizeof(float ));
		fftObj->wSinArr1=(float *)calloc(length, sizeof(float ));
		_createWArr1(fftObj->wCosArr1, fftObj->wSinArr1, length);
	}

	wCosArr1=fftObj->wCosArr1;
	wSinArr1=fftObj->wSinArr1;

	_realArr1=fftObj->realArr1;
	_imageArr1=fftObj->imageArr1;

	_realArr2=fftObj->realArr2;
	_imageArr2=fftObj->imageArr2;

	fftObj->rFlag=1;

	memset(_imageArr1,0,sizeof(float )*length);
	for(int i=0;i<length/2;i++){
		_realArr1[i]=dataArr1[i*2];
		_realArr1[length-1-i]=dataArr1[i*2+1];
	}

	_fftObj_fft(fftObj,_realArr1,_imageArr1,dataArr2,_imageArr2, 0);
	_vmulReal(dataArr2,_imageArr2,wCosArr1,wSinArr1,length);

	if(isNorm){
		dataArr2[0]=dataArr2[0]*fftObj->s0;
		for(int i=1;i<length;i++){
			dataArr2[i]=dataArr2[i]*fftObj->s1;
		}
	}

	fftObj->execType=FFTExec_DCT;
	fftObj->rFlag=0;
}

void fftObj_idct(FFTObj fftObj,float *dataArr1,float *dataArr2,int isNorm){
	int length=0;

	float *wCosArr1=NULL;
	float *wSinArr1=NULL;

	float *_realArr1=NULL;
	float *_imageArr1=NULL;

	float *_realArr2=NULL;
	float *_imageArr2=NULL;

	length=fftObj->fftLength;

	if(!fftObj->wCosArr1){
		fftObj->wCosArr1=(float *)calloc(length, sizeof(float ));
		fftObj->wSinArr1=(float *)calloc(length, sizeof(float ));
		_createWArr1(fftObj->wCosArr1, fftObj->wSinArr1, length);
	}

	wCosArr1=fftObj->wCosArr1;
	wSinArr1=fftObj->wSinArr1;

	_realArr1=fftObj->realArr1;
	_imageArr1=fftObj->imageArr1;

	_realArr2=fftObj->realArr2;
	_imageArr2=fftObj->imageArr2;

	if(isNorm){
		dataArr1[0]/=fftObj->s0;
		for(int i=1;i<length;i++){
			dataArr1[i]/=fftObj->s1;
		}
	}

	dataArr1[0]/=2;
	for(int i=0;i<length;i++){
		dataArr1[i]/=fftObj->wLength;
		_realArr1[i]=dataArr1[i]*wCosArr1[i];
		_imageArr1[i]=dataArr1[i]*wSinArr1[i];
	}

	_fftObj_fft(fftObj,_realArr1,_imageArr1,_realArr2,_imageArr2,0);

	for(int i=0;i<length/2;i++){
		dataArr2[i*2]=_realArr2[i];
		dataArr2[i*2+1]=_realArr2[length-1-i];
	}

	fftObj->execType=FFTExec_IDCT;
}

int fftObj_getFFTLength(FFTObj fftObj){

	return fftObj->fftLength;
}

void fftObj_debug(FFTObj fftObj){
	float *realArr2=NULL;
	float *imageArr2=NULL;
	int length=0;

	length=fftObj->fftLength;

	realArr2=fftObj->realArr2;
	imageArr2=fftObj->imageArr2;

	if(fftObj->execType!=FFTExec_None){
		if(fftObj->execType==FFTExec_FFT){
			printf("fft ");
		}
		else if(fftObj->execType==FFTExec_IFFT){
			printf("ifft ");
		}
		else if(fftObj->execType==FFTExec_DCT){
			printf("dct ");
		}
		else if(fftObj->execType==FFTExec_IDCT){
			printf("idct ");
		}

		printf("result is: \n");
		for(int i=0;i<length;i++){
			printf("index %d: %f %f\n",i,realArr2[i],imageArr2[i]);
		}
	}
}

void fftObj_free(FFTObj fftObj){
	int *indexArr=NULL; // reverse order cache

	float *wCosArr=NULL; // w cache
	float *wSinArr=NULL;

	float *wCosArr1=NULL;
	float *wSinArr1=NULL;

	float *realArr1=NULL;
	float *imageArr1=NULL;

	float *realArr2=NULL;
	float *imageArr2=NULL;

	if(!fftObj){
		return;
	}

	indexArr=fftObj->indexArr;

	wCosArr=fftObj->wCosArr;
	wSinArr=fftObj->wSinArr;

	wCosArr1=fftObj->wCosArr1;
	wSinArr1=fftObj->wSinArr1;

	realArr1=fftObj->realArr1;
	imageArr1=fftObj->imageArr1;

	realArr2=fftObj->realArr2;
	imageArr2=fftObj->imageArr2;

	free(indexArr);

	free(wCosArr);
	free(wSinArr);

	free(wCosArr1);
	free(wSinArr1);

	free(realArr1);
	free(imageArr1);

	free(realArr2);
	free(imageArr2);

	#ifdef HAVE_ACCELERATE
	vDSP_destroy_fftsetup(fftObj->setup);

	#elif defined HAVE_FFTW3F
	fftwf_destroy_plan(fftObj->planReal);
	fftwf_destroy_plan(fftObj->planComplex);
	fftwf_destroy_plan(fftObj->planInverse);

	fftwf_free(fftObj->inData1);
	fftwf_free(fftObj->outData1);

	fftwf_free(fftObj->inData2);
	fftwf_free(fftObj->outData2);

	fftwf_free(fftObj->inData3);
	fftwf_free(fftObj->outData3);

	#elif defined HAVE_MKL
	DftiFreeDescriptor(&fftObj->handleReal);
	DftiFreeDescriptor(&fftObj->handleComplex);
	DftiFreeDescriptor(&fftObj->handleInverse);

	free(fftObj->outData1);

	mkl_free(fftObj->inData2);
	mkl_free(fftObj->outData2);

	mkl_free(fftObj->inData3);
	mkl_free(fftObj->outData3);

	#endif

	free(fftObj);
}

static int *_createIndexArr(int n,int length){
	int *indexArr=NULL;
	int *arr;

	int j=0;
	int k=0;

	int _v=0;

	indexArr=(int *)calloc(length,sizeof(int ));
	arr=(int *)calloc(length,sizeof(int ));
	for(int i=0;i<length;i++){
		arr[i]=i;
	}

	for(int i=0;i<length;i++){
		j=0;
		k=0;
		do{
			_v=(i>>(j++))&0x01;
			k=k|_v;
			if(j<n){
				k=k<<1;
			}
		}while(j<n);

		if(k<length){
			indexArr[k]=arr[i];
		}
	}

	free(arr);
	return indexArr;
}

static void _createWArr(float *wCosArr,float *wSinArr,int wLength){
	int length=0;

	length=2*wLength;
	for(int i=0;i<wLength;i++){
		wCosArr[i]=cosf(2*M_PI*i/length);
		wSinArr[i]=-sinf(2*M_PI*i/length);
	}

}

static void _createWArr1(float *wCosArr,float *wSinArr,int wLength){
	int length=0;

	length=2*wLength;
	for(int i=0;i<wLength;i++){
		wCosArr[i]=cosf(M_PI*i/length);
		wSinArr[i]=-sinf(M_PI*i/length);
	}
}

static void _vmulReal(float *realArr,float *imageArr,float *wCosArr,float *wSinArr,int length){

	for(int i=0;i<length;i++){
		realArr[i]=realArr[i]*wCosArr[i]-imageArr[i]*wSinArr[i];
	}
}




```

---

### Archivo: `./src/dsp/phase_vocoder.h`

```


#ifndef PHASE_VOCODER_H
#define PHASE_VOCODER_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

/***
	mDataArr1 stft time*fftLength
	rate 0.5~2
	slideLength fftLength/4
****/
void phase_vocoder(float *mRealArr1,float *mImageArr1,int timeLength,int fftLength,int slideLength,float rate,
				float *mRealArr2,float *mImageArr2);


#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/dsp/flux_window.h`

```


#ifndef FLUX_WINDOW_H
#define FLUX_WINDOW_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#include "../flux_base.h"

// 窗函数相关 flag 0 symmetric对称 1 periodic周期 针对fft length extend 1 sample
float *window_createHann(int length,int flag);
float *window_createHamm(int length,int flag);

float *window_createBlackman(int length,int flag);
// beta 5.0
float *window_createKaiser(int length,int flag,float *beta);

// only symmetric
float *window_createBartlett(int length,int flag);
float *window_createTriang(int length,int flag);

float *window_createFlattop(int length,int flag);
// alpha 2.5
float *window_createGauss(int length,int flag,float *alpha);

// 4-term blackman harris~nuttall
float *window_createBlackmanHarris(int length,int flag);
float *window_createBlackmanNuttall(int length,int flag);
// like Bartlett,hann,hamm; only symmetric
float *window_createBartlettHann(int length,int flag);

// only symmetric
float *window_createBohman(int length,int flag);

// alpha>=0&&<=1 0.5 rect~hann ;only symmetric
float *window_createTukey(int length,int flag,float *alpha);

// order相关 
// w1 ws/wp w2 ws/wp atten dB
void window_calKaiserOrder(float w1,float w2,float atten,int *order,float *beta);

float *window_calFFTWindow(WindowType type,int length);


#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/dsp/fft_algorithm.h`

```
// clang -g 

#ifndef FFT_ALGORITHM_H
#define FFT_ALGORITHM_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "../flux_base.h"

typedef enum{
	FFTParamError=-100,
	FFTExecError=-101,

} FFTError;

typedef struct OpaqueFFT *FFTObj;

int fftObj_new(FFTObj *fftObj,int radix2Exp);

int fftObj_getFFTLength(FFTObj fftObj);

void fftObj_fft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2);
void fftObj_ifft(FFTObj fftObj,float *realArr1,float *imageArr1,float *realArr2,float *imageArr2);
void fftObj_dct(FFTObj fftObj,float *dataArr1,float *dataArr2,int isNorm);
void fftObj_idct(FFTObj fftObj,float *dataArr1,float *dataArr2,int isNorm);

void fftObj_free(FFTObj fftObj);
void fftObj_debug(FFTObj fftObj);

#ifdef __cplusplus
}
#endif

#endif

```

---

### Archivo: `./src/flux_spectral.h`

```


#ifndef FLUX_SPECTRAL_H
#define FLUX_SPECTRAL_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "flux_base.h"

void spectral_flatness(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,
					float *vArr);

// step >=1;type 0(default) sum 1 mean
void spectral_flux(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					int step,float p,int isPostive,int isExp,int type,
					float *vArr);

void spectral_rolloff(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,float threshold,
					float *vArr);

void spectral_centroid(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,
					float *vArr);

void spectral_spread(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,float *cArr,
					float *vArr);

void spectral_skewness(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,float *cArr1,float *cArr2,
					float *vArr);

void spectral_kurtosis(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,float *cArr1,float *cArr2,
					float *vArr);

// 1 matlab 0 song
void spectral_entropy(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *sumArr,int isNorm,
					float *vArr);

void spectral_crest(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *sumArr,
					float *vArr);

void spectral_slope(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *meanFreArr,float *meanValueArr,
					float *vArr);

void spectral_decrease(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *sumArr,
					float *vArr);

void spectral_bandWidth(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float *freArr,float *cArr,float p,
					float *vArr);

void spectral_rms(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr);


// ['hfc', 'sd', 'sf', 'mkl', 'pd', 'wpd', 'nwpd', 'cd', 'rcd']
void spectral_hfc(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr);

void spectral_sd(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				int step,int isPostive,
				float *vArr);

void spectral_sf(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				int step,int isPostive,
				float *vArr);

// type 0 sum 1 mean
void spectral_mkl(float *mDataArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				int type,
				float *vArr);

void spectral_pd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr);

void spectral_wpd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr);

void spectral_nwpd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr);

void spectral_cd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr);

void spectral_rcd(float *mSpecArr,float *mPhaseArr,int nLength,int mLength,
				int *indexArr,int indexLength,
				float *vArr);

// threshold 0/3/6  
void spectral_broadband(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					float threshold,
					float *vArr);

/***
	step >=1
	threshold 0
	methodType 'sub'
	dataType 'value'
****/
void spectral_novelty(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					int step,float threshold,
					SpectralNoveltyMethodType *methodType,SpectralNoveltyDataType *dataType,
					float *vArr);

void spectral_energy(float *mDataArr,int nLength,int mLength,
					int *indexArr,int indexLength,
					int isPower,int isLog,float gamma,
					float *vArr);


#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/cqt_algorithm.h`

```


#ifndef CQT_ALGORITHM_H
#define CQT_ALGORITHM_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "flux_base.h"

typedef struct OpaqueCQT *CQTObj;

int cqtObj_new(CQTObj *cqtObj,int num,int samplate,float minFre,int *isContinue);
/***
	num n*binPerOctave
	samplate 32000
	minFre C1=32.703
	binPerOctave 12
	factor 1 
		>0  <1 short window
	beta 0 
		>=0 0 cqt >0 vqt ???
	thresh 0.01
	windowType 'hann'
	slideLength fftLength/4
	isScale 1
****/
int cqtObj_newWith(CQTObj *cqtObj,int num,
				int *samplate,float *minFre,int *binPerOctave,
				float *factor,float *beta,float *thresh,
				WindowType *windowType,int *slideLength,int *isContinue,
				SpectralFilterBankNormalType *filterNormalType,int *isScale);

int cqtObj_calTimeLength(CQTObj cqtObj,int dataLength);
int cqtObj_getFFTLength(CQTObj cqtObj);
// num
float *cqtObj_getFreBandArr(CQTObj cqtObj);

void cqtObj_setScale(CQTObj cqtObj,int flag);

void cqtObj_cqt(CQTObj cqtObj,float *dataArr,int dataLength,float *mRealArr,float *mImageArr);
/***
	chromaNum 12
	dataType 'power' mag||power 
	mDataArr timeLength*chromaNum
	normType 'Max'
****/
void cqtObj_chroma(CQTObj cqtObj,int *chromaNum,SpectralDataType *dataType,ChromaDataNormalType *normType,
				float *mRealArr,float *mImageArr,
				float *mDataArr);

// mDataArr1  "mag" mag||power
void cqtObj_cqcc(CQTObj cqtObj,float *mDataArr1,int ccNum,CepstralRectifyType *rectifyType,float *mDataArr2);

// mDataArr1  "power" mag||power
void cqtObj_cqhc(CQTObj cqtObj,float *mDataArr1,int hcNum,float *mDataArr2);
// mDataArr1  "mag" mag||power
void cqtObj_deconv(CQTObj cqtObj,float *mDataArr1,float *mDataArr2,float *mDataArr3);

void cqtObj_free(CQTObj cqtObj);



#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/mir/onset_algorithm.c`

```
// 

#include <string.h>
#include <math.h>

#include "../vector/flux_vector.h"
#include "../vector/flux_vectorOp.h"

#include "../util/flux_util.h"

#include "../flux_spectral.h"

#include "onset_algorithm.h"

struct OpaqueOnset{
	NoveltyType noveltyType;

	int nLength; // timeLength
	int mLength; // freLength

	int order; // fre

	int preMax;
	int postMax;

	int preAvg;
	int postAvg;
	
	int wait;
	float delta;

	float *mFilterArr; // nLength*mLength
	float *mFluxArr; // (nLength-step)*mLength

	// novelty params
	int step;
	float p;
	int isPostive;
	int isExp;
	int type;

	float threshold;

	int isNorm;
	float gamma;
	
};

static void _onsetObj_dealFilterArr(OnsetObj onsetObj,float *mDataArr1);
static void _onsetObj_dealFluxArr(OnsetObj onsetObj,float *mDataArr1,float *mDataArr2,int *indexArr,int indexLength,float *vArr1);
static int _onsetObj_dealPointArr(OnsetObj onsetObj,float *evnArr,int *pointArr);

static void _onsetObj_initPeak(OnsetObj onsetObj,int samplate,int slideLength);
static void _onsetObj_initParam(OnsetObj onsetObj,NoveltyParam *param);

static int __peakPick(float *evnArr,int *pointArr,int length,int preMax,int postMax,int preAvg,int postAvg,int wait,float delta);

int onsetObj_new(OnsetObj *onsetObj,int nLength,int mLength,int slideLength,
				int *samplate,int *filterOrder,
				NoveltyType *type){
	int status=0;

	NoveltyType _type=Novelty_Flux;

	int order=1;

	float *mFluxArr=NULL;
	float *mFilterArr=NULL;

	int _samplate=32000;

	OnsetObj onset=NULL;

	onset=*onsetObj=(OnsetObj )calloc(1,sizeof(struct OpaqueOnset ));

	if(type){
		_type=*type;
	}

	if(filterOrder){
		if(*filterOrder>0){
			order=*filterOrder;
		}
	}

	if(samplate){
		if(*samplate>0){
			_samplate=*samplate;
		}
	}

	if(slideLength<1){
		slideLength=512;
	}

	mFluxArr=__vnew(nLength*mLength, NULL);
	mFilterArr=__vnew(nLength*mLength, NULL);

	onset->noveltyType=_type;

	onset->nLength=nLength;
	onset->mLength=mLength;

	onset->order=order;

	onset->mFluxArr=mFluxArr;
	onset->mFilterArr=mFilterArr;
	
	_onsetObj_initPeak(onset,_samplate,slideLength);

	return status;
}

/***
	large-scale from CPJKU onset_db
	preMax 0.03*sr/slideLength
	postMax 0.00*sr/slideLength+1
	preAvg 0.1*sr/slideLength
	postAvg 0.1*sr/slideLength+1
	wait 0.03*sr/slideLength
	delta 0.07
****/
static void _onsetObj_initPeak(OnsetObj onsetObj,int samplate,int slideLength){

	onsetObj->preMax=floorf(0.03*samplate/slideLength);
	onsetObj->postMax=floorf(0.0*samplate/slideLength+1);

	onsetObj->preAvg=floorf(0.1*samplate/slideLength);
	onsetObj->postAvg=floorf(0.1*samplate/slideLength+1);

	onsetObj->wait=floorf(0.03*samplate/slideLength);
	onsetObj->delta=0.07;
}

static void _onsetObj_initParam(OnsetObj onsetObj,NoveltyParam *param){
	int step=1;
	float p=1;
	int isPostive=1;
	int isExp=0;
	int type=0;

	float threshold=0;

	int isNorm=0;
	float gamma=1;

	if(param){
		if(param->step>0){
			step=param->step;
		}

		if(param->p){ // !=0
			p=param->p;
		}

		isPostive=param->isPostive;
		isExp=param->isExp;
		type=param->type;

		threshold=param->threshold;

		isNorm=param->isNorm;
		if(param->gamma>0){
			gamma=param->gamma;
		}
	}


	onsetObj->step=step;
	onsetObj->p=p;
	onsetObj->isPostive=isPostive;
	onsetObj->isExp=isExp;
	onsetObj->type=type;

	onsetObj->threshold=threshold;

	onsetObj->isNorm=isNorm;
	onsetObj->gamma=gamma;
}

/***
	1. cal evnArr
	2. cal pointArr
****/
int onsetObj_onset(OnsetObj onsetObj,float *mDataArr1,float *mDataArr2,
				NoveltyParam *param,int *indexArr,int indexLength,
				float *evnArr,int *pointArr){
	int pointLength=0;

	int *iArr=NULL;
	int iLength=0;

	if(indexArr){
		iArr=__vnewi(indexLength, NULL);
		memcpy(iArr, indexArr, sizeof(int )*indexLength);
		iLength=indexLength;
	}
	else{
		__varangei(0, onsetObj->mLength, 1, &iArr);
		iLength=onsetObj->mLength;
	}

	_onsetObj_initParam(onsetObj, param);

	_onsetObj_dealFilterArr(onsetObj,mDataArr1);
	_onsetObj_dealFluxArr(onsetObj,mDataArr1,mDataArr2,iArr,iLength,evnArr);
	pointLength=_onsetObj_dealPointArr(onsetObj,evnArr,pointArr);

	free(iArr);
	return pointLength;
}

static int _onsetObj_dealPointArr(OnsetObj onsetObj,float *evnArr,int *pointArr){
	int pointLength=0;
	int length=0;

	int preMax=0;
	int postMax=0;
	int preAvg=0;
	int postAvg=0;
	int wait=0;
	float delta=0;

	length=onsetObj->nLength;

	preMax=onsetObj->preMax;
	postMax=onsetObj->postMax;
	preAvg=onsetObj->preAvg;
	postAvg=onsetObj->postAvg;
	delta=onsetObj->delta;
	wait=onsetObj->wait;

	pointLength=__peakPick(evnArr, pointArr, length, preMax, postMax, preAvg, postAvg,wait,delta);

	return pointLength;
}

static void _onsetObj_dealFilterArr(OnsetObj onsetObj,float *mDataArr1){
	int nLength=0; // timeLength
	int mLength=0; // freLength

	int order=0; // fre

	float *mFilterArr=NULL; // nLength*mLength

	order=onsetObj->order;
	if(order<2){
		return;
	}

	nLength=onsetObj->nLength;
	mLength=onsetObj->mLength;

	mFilterArr=onsetObj->mFilterArr;

	__mmaxfilter(mDataArr1,nLength,mLength,1,order,mFilterArr);
}

static void _onsetObj_dealFluxArr(OnsetObj onsetObj,float *mDataArr1,float *mDataArr2,int *indexArr,int indexLength,float *vArr1){
	NoveltyType noveltyType=Novelty_Flux;

	int nLength=0; // timeLength
	int mLength=0; // freLength

	int order=0; // fre

	float *mFluxArr=NULL; // (nLength-step)*mLength
	float *mArr=NULL;

	float min=0;
	float max=0;

	int step=1; // >=1
	float p=1; // >=1
	int isPostive=1; // 1
	int isExp=0; // 0
	int type=0; // 0 sum 1 mean

	float threshold=0; // >=0

	int isNorm=0; // 0|1
	float gamma=1;

	int start=0;
	int end=0;

	noveltyType=onsetObj->noveltyType;

	nLength=onsetObj->nLength;
	mLength=onsetObj->mLength;

	order=onsetObj->order;

	mFluxArr=onsetObj->mFluxArr;
	if(order>1){
		mArr=onsetObj->mFilterArr;
	}
	else{
		mArr=mDataArr1;
	}

	start=0;
	end=nLength-1;

	step=onsetObj->step;
	p=onsetObj->p;
	isPostive=onsetObj->isPostive;
	isExp=onsetObj->isExp;
	type=onsetObj->type;

	threshold=onsetObj->threshold;

	isNorm=onsetObj->isNorm;
	gamma=onsetObj->gamma;

	memset(vArr1, 0, sizeof(float )*step);
	
	if(noveltyType==Novelty_HFC){
		spectral_hfc(mArr,nLength,mLength,
					indexArr,indexLength,
					vArr1);
	}
	else if(noveltyType==Novelty_SD){
		spectral_sd(mArr,nLength,mLength,
					indexArr,indexLength,
					step,isPostive,
					vArr1);
	}
	else if(noveltyType==Novelty_SF){
		spectral_sf(mArr,nLength,mLength,
					indexArr,indexLength,
					step,isPostive,
					vArr1);
	}
	else if(noveltyType==Novelty_MKL){
		spectral_mkl(mArr,nLength,mLength,
					indexArr,indexLength,
					type,
					vArr1);
	}
	else if(noveltyType==Novelty_PD){
		spectral_pd(mArr,mDataArr2,nLength,mLength,
					indexArr,indexLength,
					vArr1);
	}
	else if(noveltyType==Novelty_WPD){
		spectral_wpd(mArr,mDataArr2,nLength,mLength,
					indexArr,indexLength,
					vArr1);
	}
	else if(noveltyType==Novelty_NWPD){
		spectral_nwpd(mArr,mDataArr2,nLength,mLength,
					indexArr,indexLength,
					vArr1);
	}
	else if(noveltyType==Novelty_CD){
		spectral_cd(mArr,mDataArr2,nLength,mLength,
					indexArr,indexLength,
					vArr1);
	}
	else if(noveltyType==Novelty_RCD){
		spectral_rcd(mArr,mDataArr2,nLength,mLength,
					indexArr,indexLength,
					vArr1);
	}
	else if(noveltyType==Novelty_Broadband){
		spectral_broadband(mArr,nLength,mLength,
							indexArr,indexLength,
							threshold,
							vArr1);
	}
	else{ // flux
		spectral_flux(mArr,nLength,mLength,
					indexArr,indexLength,
					step,p,isPostive,isExp,type,
					vArr1);
	}

	__vmin(vArr1, nLength, &min);
	__vsub_value(vArr1, min, nLength, vArr1);

	__vmax(vArr1, nLength, &max);
	if(max>0){
		__vdiv_value(vArr1, max, nLength, vArr1);
	}
}

void onsetObj_free(OnsetObj onsetObj){
	float *mFilterArr=NULL; // nLength*mLength
	float *mFluxArr=NULL; // (nLength-step)*mLength

	if(!onsetObj){
		return;
	}

	mFilterArr=onsetObj->mFilterArr;
	mFluxArr=onsetObj->mFluxArr;

	free(mFilterArr);
	free(mFluxArr);

	free(onsetObj);
}

void onsetObj_debug(OnsetObj onsetObj){

	printf("onsetObj is :\n");
	printf("preMax=%d,postMax=%d, preAvg=%d,postAvg=%d, wait=%d,delta=%f\n",
			onsetObj->preMax,onsetObj->postMax,onsetObj->preAvg,onsetObj->postAvg,onsetObj->wait,onsetObj->delta);

	printf("timeLength=%d,freNum=%d, step=%d,order=%d\n",
			onsetObj->nLength,onsetObj->mLength,onsetObj->step,onsetObj->order);

	printf("\n");
}

// peak
/***
	x[n]==max(x[n-preMax:n+postMax]) &&
	x[n]>=mean(x[n-preAvg:n+postAvg])+delta &&
	n-pre>wait => n is point
****/
static int __peakPick(float *evnArr,int *pointArr,int length,int preMax,int postMax,int preAvg,int postAvg,int wait,float delta){
	int pointLength=0;

	int pre=0;

	float max=0;
	float mean=0;

	int start1=0;
	int end1=0;

	int start2=0;
	int end2=0;

	pre=-wait-1;
	for(int i=0;i<length;i++){
		start1=(i-preMax>=0?i-preMax:0);
		end1=(i+postMax<length?i-1+postMax:length-1);

		__vmax(evnArr+start1, end1-start1+1, &max);
		if(evnArr[i]==max){
			start2=(i-preAvg>=0?i-preAvg:0);
			end2=(i+postAvg<length?i-1+postAvg:length-1);

			mean=__vmean(evnArr+start2, end2-start2+1);
			if(evnArr[i]>=mean+delta){
				if(i-pre>wait){
					pointArr[pointLength]=i;
					pre=i;

					pointLength++;
				}
			}
		}
	}

	return pointLength;
}


```

---

### Archivo: `./src/mir/_queue.h`

```


#ifndef _PITCH_UTIL_H
#define _PITCH_UTIL_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

float __queue_fre3(float value1,float value2,float value3,
					int *s1,int *s2,
					int *k1,int *k2,int *k3);

float __queue_fre2(float value1,float value2,
					int *k1,int *k2);

#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/mir/_queue.c`

```
// 

#include <string.h>
#include <math.h>

#include "../vector/flux_vector.h"
#include "../vector/flux_vectorOp.h"
#include "../vector/flux_complex.h"

#include "../util/flux_util.h"

#include "_queue.h"

/***
	1:1/1:2/1:3 2:2 2:3
	1:4 ???
****/
float __queue_fre3(float value1,float value2,float value3,
					int *s1,int *s2,
					int *k1,int *k2,int *k3){
	float base=0;

	float sub1=0;
	float sub2=0;
	float _sub=0;

	int _k=0;
	int _k1=0;
	int _k2=0;
	int _k3=0;

	int _s1=0;
	int _s2=0;

	int gFlag=0;
	int type=0;

	sub1=value2-value1;
	sub2=value3-value2;
	if(sub1>sub2){
		_sub=sub1;
		sub1=sub2;
		sub2=_sub;

		gFlag=1;
	}

	_k=util_calRangeTimes(sub1,sub2,&type);
	if(_k==1){ // 1:1
		_k1=util_calRangeTimes(sub1,value1,&type);
		_k2=util_calRangeTimes(sub1,value2,&type);
		if(_k1&&_k2){ 
			// _k3=util_calRangeTimes(sub1,value3,&type);
			_k3=_k2+1;

			_s1=1;
			_s2=1;

			base=value1/_k1;
		}
		else{ // 2:2
			_k1=util_calRangeTimes(sub1/2,value1,&type);
			_k2=util_calRangeTimes(sub1/2,value2,&type);
			if(_k1&&_k2){
				// _k3=util_calRangeTimes(sub1/2,value3,&type);
				_k3=_k2+2;

				if(_k1%2==1){ // ->2:2
					_s1=2;
					_s2=2;

					base=value1/_k1;
				}
				else{ // ->1:1
					_s1=1;
					_s2=1;

					_k1/=2;
					_k2/=2;
					_k3/=2;

					base=value1/_k1;
				}
			}
		}
	}
	else if(_k>=2&&_k<=4){ // 1:2 1:3 1:4
		_k1=util_calRangeTimes(sub1,value1,&type);
		_k2=util_calRangeTimes(sub1,value2,&type);
		if(_k1&&_k2){
			// _k3=util_calRangeTimes(sub1,value3,&type);
			if(gFlag){
				_k3=_k2+1;
			}
			else{
				_k3=_k2+_k;
			}

			_s1=(gFlag?_k:1);
			_s2=(gFlag?1:_k);

			base=value1/_k1;
		}
	}
	else{ // 2:3
		_sub=sub2-sub1;
		_k1=util_calRangeTimes(_sub,sub1,&type);
		_k2=util_calRangeTimes(_sub,sub2,&type);
		if(_k1==2&&_k2==3){
			_k1=util_calRangeTimes(sub1/2,value1,&type);
			_k2=util_calRangeTimes(sub1/2,value2,&type);
			if(_k1&&_k2){
				// _k3=util_calRangeTimes(sub1/2,value3,&type);
				if(gFlag){
					_k3=_k2+2;
				}
				else{
					_k3=_k2+3;
				}

				_s1=(gFlag?3:2);
				_s2=(gFlag?2:3);

				base=value1/_k1;
			}
		}
	}

	if(!base){
		_k=roundf(sub2/sub1);
		if(_k==1){ // 1:1
			_k1=roundf(value1/sub1);
			_k2=roundf(value2/sub1);
			if(_k1+1==_k2){ 
				// _k3=util_calRangeTimes(sub1,value3,&type);
				_k3=_k2+1;

				_s1=1;
				_s2=1;

				base=value1/_k1;
			}
			else{ // 2:2
				_k1=roundf(value1/(sub1/2));
				_k2=roundf(value2/(sub1/2));
				if(_k1+2==_k2){
					// _k3=util_calRangeTimes(sub1/2,value3,&type);
					_k3=_k2+2;

					_s1=2;
					_s2=2;

					base=value1/_k1;
				}
			}
		}
		else if(_k>=2&&_k<=4){ // 1:2 1:3 1:4
			_k1=roundf(value1/sub1);
			_k2=roundf(value2/sub1);
			if(_k1&&_k2){
				// _k3=util_calRangeTimes(sub1,value3,&type);
				if(gFlag){
					_k3=_k2+1;
				}
				else{
					_k3=_k2+_k;
				}

				_s1=(gFlag?_k:1);
				_s2=(gFlag?1:_k);

				base=value1/_k1;
			}
		}

		if(base){
			if(!(fabsf(value2-value1/_k1*_k2)<5&&
				fabsf(value3-value1/_k1*_k3)<5)){

				base=0;
			}
		}
	}

	if(base){
		if(s1){
			*s1=_s1;
		}
		if(s2){
			*s2=_s2;
		}

		if(k1){
			*k1=_k1;
		}
		if(k2){
			*k2=_k2;
		}
		if(k3){
			*k3=_k3;
		}
	}
	else{
		if(s1){
			*s1=0;
		}
		if(s2){
			*s2=0;
		}

		if(k1){
			*k1=0;
		}
		if(k2){
			*k2=0;
		}
		if(k3){
			*k3=0;
		}
	}

	return base;
}

/***
	k=value2/value1
	1:n/2:n
****/
float __queue_fre2(float value1,float value2,
					int *k1,int *k2){
	float fre=0;

	int type=0;
	
	int k=0;
	int _k1=0;
	int _k2=0;

	float sub=0;

	int flag=0;

	// k=util_calFreTimes(value1,value2,NULL);
	k=util_calRangeTimes(value1,value2,NULL);
	if(k){ // >=1
		fre=value1;

		_k1=1;
		_k2=k;
	}
	else{
		sub=value2-value1;

		_k2=util_calRangeTimes(sub,value2,NULL);
		if(_k2){
			_k1=util_calRangeTimes(sub,value1,&type);
			if(_k1&&!type){
				fre=value1/_k1;

				flag=1;
			}
		}

		if(!flag){
			sub/=2;
			_k2=util_calRangeTimes(sub,value2,NULL);
			if(_k2){
				_k1=util_calRangeTimes(sub,value1,&type);
				if(_k1&&!type){
					fre=value1/_k1;
				}
			}
		}
	}

	if(fre){
		if(k1){
			*k1=_k1;
		}
		if(k2){
			*k2=_k2;
		}
	}
	else{
		if(k1){
			*k1=0;
		}
		if(k2){
			*k2=0;
		}
	}

	return fre;
}











```

---

### Archivo: `./src/mir/onset_algorithm.h`

```


#ifndef ONSET_ALGORITHM_H
#define ONSET_ALGORITHM_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

typedef enum{
	Novelty_Flux=0,

	Novelty_HFC,
	Novelty_SD,
	Novelty_SF,
	Novelty_MKL,

	Novelty_PD,
	Novelty_WPD, 
	Novelty_NWPD, 

	Novelty_CD, 
	Novelty_RCD, 

	Novelty_Broadband,

} NoveltyType;

typedef struct {
	int step; // >=1
	float p; // 1 !=0
	int isPostive; // 1
	int isExp; // 0
	int type; // 0 sum 1 mean

	float threshold; // >=0

	int isNorm; // 0|1
	float gamma; // 1 0.5/1/10/20...

} NoveltyParam;

typedef struct OpaqueOnset *OnsetObj;

/***
	samplate 32000
	filterOrder 1
	type Novelty_Flux
****/
int onsetObj_new(OnsetObj *onsetObj,int nLength,int mLength,int slideLength,
				int *samplate,int *filterOrder,
				NoveltyType *type);

int onsetObj_onset(OnsetObj onsetObj,float *mDataArr1,float *mDataArr2,
				NoveltyParam *param,int *indexArr,int indexLength,
				float *evnArr,int *pointArr);

void onsetObj_free(OnsetObj onsetObj);
void onsetObj_debug(OnsetObj onsetObj);

#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/reassign_algorithm.h`

```


#ifndef REASSIGN_ALGORITHM_H
#define REASSIGN_ALGORITHM_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "flux_base.h"

typedef enum{
	Reassign_All=0,

	Reassign_Fre, 
	Reassign_Time, 

	Reassign_None, 
	
} ReassignType;

typedef struct OpaqueReassign *ReassignObj;

/***
	radix2Exp 12
	samplate 32000
	windowType 'hann'
	slideLength fftLength/4

	reType Reassign_All
	thresh 0.001 
	
	isPadding 0
	isContinue 0
****/
int reassignObj_new(ReassignObj *reassignObj,int radix2Exp,
					int *samplate,WindowType *windowType,int *slideLength,
					ReassignType *reType,float *thresh,
					int *isPadding,int *isContinue);

int reassignObj_calTimeLength(ReassignObj reassignObj,int dataLength);

// 0 complex,1 real ->mRealArr1(amp)
void reassignObj_setResultType(ReassignObj reassignObj,int type);
// order >=1
void reassignObj_setOrder(ReassignObj reassignObj,int order);

// mRealArr2&mImageArr2 may NULL
void reassignObj_reassign(ReassignObj reassignObj,float *dataArr,int dataLength,
						float *mRealArr1,float *mImageArr1,
						float *mRealArr2,float *mImageArr2);

void reassignObj_free(ReassignObj reassignObj);


#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/filterbank/cqt_filterBank.c`

```
// clang 

#include <string.h>
#include <math.h>

#include "../vector/flux_vector.h"
#include "../vector/flux_vectorOp.h"
#include "../vector/flux_complex.h"

#include "../util/flux_util.h"

#include "../dsp/flux_window.h"
#include "../dsp/fft_algorithm.h"

#include "cqt_filterBank.h"

// tempKernel
static void __cqt_calTempArr(int num,float *freBandArr, int samplate,
				float *lenArr,int fftLength,
				SpectralFilterBankNormalType normType,WindowType *winType,
				float *mReaArr,float *mImageArr);

// 0 fftLength/2+1 1 fftLength
static void __cqt_filterBank(int num,float *freBandArr,int samplate,
				int binPerOctave,SpectralFilterBankNormalType normType,WindowType *winType,
				float *factor,float *beta,float *thresh,
				float *lenArr,int fftLength,
				float *mRealFilterBankArr,float *mImageFilterBankArr,int type);

// filterBank相关
/***
	cqt filterBank 基于音乐octave分割的freBandArr
		normType 归一化方式 ???
		winType 'hann' paper 'hamm'
		factor 1 调节时间分辨率 
		beta 0 调节可变Q
		thresh 0.01 paper 0.0054
	1. tempKernel计算
	2. freKernel计算
	3. 阈值过滤
	mFilterBankArr=>num*(fftLength/2+1) num即length 非稀疏矩阵 
****/
void cqt_filterBank(int num,float *freBandArr,int samplate,
				int binPerOctave,SpectralFilterBankNormalType normType,WindowType *winType,
				float *factor,float *beta,float *thresh,
				float *lenArr,int fftLength,
				float *mRealFilterBankArr,float *mImageFilterBankArr){

	__cqt_filterBank(num,freBandArr,samplate,
					binPerOctave,normType,winType,
					factor,beta,thresh,
					lenArr,fftLength,
					mRealFilterBankArr,mImageFilterBankArr,
					0);
}

void cqt_downFilterBank(int num,float *freBandArr,int samplate,
				int binPerOctave,SpectralFilterBankNormalType normType,WindowType *winType,
				float *factor,float *beta,float *thresh,
				float *lenArr,int fftLength,
				float *mRealFilterBankArr,float *mImageFilterBankArr){
	int octaveNum=0; // downNum

	FFTObj fftObj=NULL;
	int m=0;

	float *mRealTempArr=NULL; // tempKernel
	float *mImageTempArr=NULL;

	float *_mRealArr1=NULL;
	float *_mImageArr1=NULL;

	float _factor=1;
	float _beta=0;
	float _thresh=0.01; // paper 0.0054
	
	if(!mRealFilterBankArr||!mImageFilterBankArr){
		return;
	}

	if(factor){
		_factor=*factor;
	}

	if(beta){
		_beta=*beta;
	}

	if(thresh){
		_thresh=*thresh;
	}

	octaveNum=num/binPerOctave;

	_mRealArr1=__vnew(num*fftLength, NULL);
	_mImageArr1=__vnew(num*fftLength, NULL);

	m=util_powerTwoBit(fftLength);
	fftObj_new(&fftObj, m);

	mRealTempArr=__vnew(binPerOctave*fftLength, NULL);
	mImageTempArr=__vnew(binPerOctave*fftLength, NULL);
	for(int i=octaveNum-1;i>=0;i--){
		// 1. tempKernel计算
		__cqt_calTempArr(binPerOctave,freBandArr+i*binPerOctave,samplate,
					lenArr,fftLength,
					normType,winType,
					mRealTempArr,mImageTempArr);

		// 2. freKernel计算
		for(int j=0;j<binPerOctave;j++){
			int index1=0;
			int index2=0;

			index1=j*fftLength;
			index2=(i*binPerOctave+j)*fftLength;
			fftObj_fft(fftObj,
					mRealTempArr+index1,mImageTempArr+index1,
					_mRealArr1+index2,_mImageArr1+index2);
		}

		samplate/=2;
	}

	// 3.阈值过滤
	_thresh*=_thresh;
	for(int i=0;i<num;i++){
		for(int j=0;j<fftLength/2+1;j++){
			float _value1=0;
			float _value2=0;

			_value1=_mRealArr1[i*fftLength+j];
			_value2=_mImageArr1[i*fftLength+j];
			if(_value1*_value1+_value2*_value2>_thresh){
				mRealFilterBankArr[i*(fftLength/2+1)+j]=_value1;
				mImageFilterBankArr[i*(fftLength/2+1)+j]=_value2;
			}
		}
	}

	free(mRealTempArr);
	free(mImageTempArr);

	free(_mRealArr1);
	free(_mImageArr1);

	fftObj_free(fftObj);
}

// factor 1.0  sacle/(2^(1/binPerOctave)-1)
float cqt_calQ(int binPerOctave,float factor){
	float q=0;

	q=factor/(powf(2, 1.0/binPerOctave)-1);
	return q;
}

// num=octaveNum*binPerOctave;
float *cqt_calFreArr(float minFre,int num,int binPerOctave){
	float *arr=NULL;

	int octaveNum=0;

	float _fre=0;
	float _value=0;

	arr=__vnew(num+2, NULL);

	octaveNum=num/binPerOctave;
	_value=powf(2, 1.0/binPerOctave);

	// arr[0]=minFre/_value;
	for(int i=0;i<octaveNum;i++){
		_fre=minFre*(1<<i);
		arr[i*binPerOctave]=_fre;
		for(int j=1;j<binPerOctave;j++){
			_fre*=_value;
			arr[i*binPerOctave+j]=_fre;
		}
	}	
	// arr[num]=arr[num-1]*_value;

	return arr;
}

// ceil(Q*fs/freArr[i])
void cqt_calLengthArr(int num,float *freBandArr,int samplate,
				int binPerOctave,
				float *factor,float *beta,
				float *lenArr){
	float q=0;
	float value=0;

	float _factor=1;
	float _beta=0;

	if(factor){
		if(*factor>0){
			_factor=*factor;
		}
	}

	if(beta){
		_beta=*beta;
	}

	value=powf(2, 1.0/binPerOctave)-1;
	q=_factor/value;
	for(int i=0;i<num;i++){
		// lenArr[i]=ceilf(q*samplate/(freBandArr[i]+_beta/value));
		lenArr[i]=q*samplate/(freBandArr[i]+_beta/value);
	}
}

int cqt_calFFTLength(float minFre,int samplate,
				int binPerOctave,
				float *factor,float *beta){
	int fftLength=0;

	float q=0;
	float value=0;

	float _factor=1;
	float _beta=0;
	int _len=0;

	if(factor){
		if(*factor>0){
			_factor=*factor;
		}
	}

	if(beta){
		_beta=*beta;
	}

	value=powf(2, 1.0/binPerOctave)-1;
	q=_factor/value;

	_len=ceilf(q*samplate/(minFre+_beta/value));
	fftLength=util_ceilPowerTwo(_len);

	return fftLength;
}

/***
	1/Nk*W[Nk]*e^(2*PI*j*n*Q/Nk) n<Nk
	W[Nk] => winType 'hann'
	1/Nk => normType
	mRealArr => num*fftLength
	1. n-range 0~n;-n/2~n/2 2. norm 1/len;util.norm 3. padding zero/center
****/
static void __cqt_calTempArr(int num,float *freBandArr, int samplate,
				float *lenArr,int fftLength,
				SpectralFilterBankNormalType normType,WindowType *winType,
				float *mReaArr,float *mImageArr){
	WindowType _winType=Window_Hann;

	if(winType){
		if(*winType!=Window_Rect){
			_winType=*winType;
		}
	}

	for(int i=0;i<num;i++){
		int len=0;
		float fre=0;

		float *arr=NULL;
		float *wArr=NULL;

		int startIndex=0;
		float weight=0;
		
		len=ceilf(lenArr[i]);
		fre=freBandArr[i];

		__varange(0, len, 1, &arr); 
		// __varange(-len/2, len/2, 1, &arr);
		// wArr=window_createHann(len, 1); // ???
		wArr=window_calFFTWindow(_winType,len);

		weight=1;
		/***
			startIndex对应arr范围 0->0~len; ((fftLength-len)/2)->-en/2~len/2 ???
			应按公式标准0~len;然后居中两边填充
		****/
		startIndex=(fftLength-len)/2;
		for(int j=0;j<len;j++){
			float value=0;

			if(normType==SpectralFilterBankNormal_None){ // same hight
				weight=lenArr[i];
			}

			value=2*M_PI*arr[j]*fre/samplate;
			mReaArr[i*fftLength+j+startIndex]=cosf(value)*wArr[j]/weight; 
			mImageArr[i*fftLength+j+startIndex]=sinf(value)*wArr[j]/weight;
		}

		// norm => 统一类auditory 归一化处理
		weight=0; // reset
		if(normType==SpectralFilterBankNormal_Area){ // sum
			for(int j=0;j<len;j++){
				float value1=0;
				float value2=0;
				
				value1=mReaArr[i*fftLength+j+startIndex];
				value2=mImageArr[i*fftLength+j+startIndex];

				weight+=sqrtf(value1*value1+value2*value2);
			}

			for(int j=0;j<len;j++){
				mReaArr[i*fftLength+j+startIndex]/=weight; 
				mImageArr[i*fftLength+j+startIndex]/=weight;
			}
		}
		else if(normType==SpectralFilterBankNormal_BandWidth){
			weight=(freBandArr[i+1]-freBandArr[i-1])/2;
			for(int j=0;j<len;j++){
				mReaArr[i*fftLength+j+startIndex]/=weight; 
				mImageArr[i*fftLength+j+startIndex]/=weight;
			}
		}

		// norm => 根据fft长度再次归一化
		for(int j=0;j<len;j++){
			mReaArr[i*fftLength+j+startIndex]*=(lenArr[i]/fftLength); 
			mImageArr[i*fftLength+j+startIndex]*=(lenArr[i]/fftLength);
		}

		free(arr);
		free(wArr);
	}
}

// type 0 fftLength/2+1 1 fftLength
static void __cqt_filterBank(int num,float *freBandArr,int samplate,
				int binPerOctave,SpectralFilterBankNormalType normType,WindowType *winType,
				float *factor,float *beta,float *thresh,
				float *lenArr,int fftLength,
				float *mRealFilterBankArr,float *mImageFilterBankArr,int type){
	FFTObj fftObj=NULL;
	int m=0;

	float *mRealTempArr=NULL; // tempKernel
	float *mImageTempArr=NULL;

	float *_mRealArr1=NULL;
	float *_mImageArr1=NULL;

	float _factor=1;
	float _beta=0;
	float _thresh=0.01; // paper 0.0054

	int mLen=0;

	if(!mRealFilterBankArr||!mImageFilterBankArr){
		return;
	}

	if(factor){
		_factor=*factor;
	}

	if(beta){
		_beta=*beta;
	}

	if(thresh){
		_thresh=*thresh;
	}

	m=util_powerTwoBit(fftLength);
	fftObj_new(&fftObj, m);

	_mRealArr1=__vnew(num*fftLength, NULL);
	_mImageArr1=__vnew(num*fftLength, NULL);

	mRealTempArr=__vnew(num*fftLength, NULL);
	mImageTempArr=__vnew(num*fftLength, NULL);

	// 1. tempKernel计算
	__cqt_calTempArr(num,freBandArr,samplate,
				lenArr,fftLength,
				normType,winType,
				mRealTempArr,mImageTempArr);

	// 2. freKernel计算
	for(int i=0;i<num;i++){
		int index=0;

		index=i*fftLength;
		fftObj_fft(fftObj,
				mRealTempArr+index,mImageTempArr+index,
				_mRealArr1+index,_mImageArr1+index);
	}

	// 3.阈值过滤
	if(!type){
		mLen=fftLength/2+1;
	}
	else{
		mLen=fftLength;
	}

	_thresh*=_thresh;
	for(int i=0;i<num;i++){
		for(int j=0;j<mLen;j++){
			float _value1=0;
			float _value2=0;

			_value1=_mRealArr1[i*fftLength+j];
			_value2=_mImageArr1[i*fftLength+j];
			if(_value1*_value1+_value2*_value2>_thresh){
				mRealFilterBankArr[i*mLen+j]=_value1;
				mImageFilterBankArr[i*mLen+j]=_value2;
			}
		}
	}

	free(mRealTempArr);
	free(mImageTempArr);

	free(_mRealArr1);
	free(_mImageArr1);

	fftObj_free(fftObj);
}




























```

---

### Archivo: `./src/filterbank/auditory_filterBank.c`

```
// 

#include <string.h>
#include <math.h>

#include "../vector/flux_vector.h"
#include "../vector/flux_vectorOp.h"
#include "../vector/flux_complex.h"

#include "../dsp/flux_window.h"
#include "../dsp/filterDesign_freqz.h"

#include "auditory_filterBank.h"

// ESTI
static void __auditory_estiFilterBank(int num,int fftLength,int isPseudo,
									SpectralFilterBankNormalType type,
									float *freBandArr,int *binBandArr,
									float *mFilterBankArr);
// Slaney
static void __auditory_slaneyFilterBank(int num,int fftLength,int samplate,int isPseudo,
									SpectralFilterBankNormalType type,
									float *freBandArr,int *binBandArr,
									float *mFilterBankArr);
// gammatone
static void __auditory_gammatoneFilterBank(int num,int fftLength,int samplate,int isPseudo,
									SpectralFilterBankNormalType type,
									float *freBandArr,int *binBandArr,
									float *mFilterBankArr);

// rect~guass 窗函数设计法
static void __auditory_windowFilterBank(int num,int fftLength,int samplate,int isPseudo,
									SpectralFilterBankStyleType styleType,
									SpectralFilterBankNormalType normType,
									float *freBandArr,int *binBandArr,
									float *mFilterBankArr);

// linear
static void __auditory_linearFilterBank(int num,int fftLength,int samplate,int isPseudo,
										float *freBandArr,int *binBandArr,
										float *mFilterBankArr);

// isEdge 0 针对非gammatone 1 gammatone
static void __auditory_calBandEdge(int num,int fftLength,int samplate,
								float lowFre,float highFre,int isEdge,int bType,
								void *callback1,void *callback2,float ref,
								float **freBandArr,int **binBandArr);

static void __reviseMidiFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3);
static void __reviseLogFre(int num,float lowFre,float highFre,int binPerOctave,int isEdge,float *lowFre3,float *highFre3);
static void __reviseLinearFre(int num,float lowFre,float highFre,float detFre,int isEdge,float *lowFre3,float *highFre3);

static void __reviseLinspaceFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3);
static void __reviseLogspaceFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3);

void auditory_filterBank(int num,int fftLength,int samplate,int isPseudo,
						SpectralFilterBankScaleType scaleType,SpectralFilterBankStyleType styleType,SpectralFilterBankNormalType normType,
						float lowFre,float highFre,int binPerOctave,
						float *mFilterBankArr,
						float *freBandArr,
						int *binBandArr){
	float *fArr=NULL;
	int *bArr=NULL;

	int isEdge=0;
	int offset=0;

	// UniFunc||UniFunc1
	void *func1=NULL;
	void *func2=NULL;

	float ref=0;
	int bType=0;

	if(styleType==SpectralFilterBankStyle_Gammatone){ // include edge!!!
		isEdge=1;
	}

	if(!isEdge){
		offset=1;
	}

	// 0. revise log/linear!!!
	if(scaleType==SpectralFilterBankScale_Octave){ 
		if(binPerOctave&&binPerOctave>=4&&binPerOctave<=48){
			ref=binPerOctave;
		}
		else{
			ref=12;
		}

		__reviseLogFre(num,lowFre,highFre,ref,isEdge,&lowFre,&highFre);
	}
	else if(scaleType==SpectralFilterBankScale_Linear){
		ref=samplate*1.0/fftLength;

		__reviseLinearFre(num,lowFre,highFre,ref,isEdge,&lowFre,&highFre);
	}
	else if(scaleType==SpectralFilterBankScale_Linspace){
		__reviseLinspaceFre(num,lowFre,highFre,isEdge,&lowFre,&highFre);
	}
	else if(scaleType==SpectralFilterBankScale_Log){
		__reviseLogspaceFre(num,lowFre,highFre,isEdge,&lowFre,&highFre);
	}

	// compatible LogChroma !!!
	if(scaleType==SpectralFilterBankScale_LogChroma){ 
		if(binPerOctave>=12&&binPerOctave%12==0){
			ref=binPerOctave;
		}
		else{
			ref=12;
		}

		__reviseLogFre(num,lowFre,highFre,ref,isEdge,&lowFre,&highFre);
	}

	// 1. freBand/binBand
	if(scaleType==SpectralFilterBankScale_Linear){ // linear
		func1=auditory_freToLinear;
		func2=auditory_linearToFre;
	}
	else if(scaleType==SpectralFilterBankScale_Linspace){ // linspace
		func1=auditory_freToLinspace;
		func2=auditory_linspaceToFre;
	}
	else if(scaleType==SpectralFilterBankScale_Mel){ // mel
		func1=auditory_freToMel;
		func2=auditory_melToFre;
	}
	else if(scaleType==SpectralFilterBankScale_Bark){ // bark
		func1=auditory_freToBark;
		func2=auditory_barkToFre;
	}
	else if(scaleType==SpectralFilterBankScale_Erb){ // erb
		func1=auditory_freToErb;
		func2=auditory_erbToFre;
	}
	else if(scaleType==SpectralFilterBankScale_Octave){ // log
		func1=auditory_freToLog;
		func2=auditory_logToFre;
	}
	else if(scaleType==SpectralFilterBankScale_Log){ // logspace
		func1=auditory_freToLogspace;
		func2=auditory_logspaceToFre;
	}
	else if(scaleType==SpectralFilterBankScale_LogChroma){ // compatible LogChroma !!!
		func1=auditory_freToLog;
		func2=auditory_logToFre;
	}

	if(styleType==SpectralFilterBankStyle_Slaney){
		bType=1;
	}

	__auditory_calBandEdge(num,fftLength,samplate,
						lowFre,highFre,isEdge,bType,
						func1,func2,ref,
						&fArr,&bArr);
	
	// 2. filterBank
	if(scaleType==SpectralFilterBankScale_Linear){
		__auditory_linearFilterBank(num,fftLength,samplate,isPseudo,
									fArr,bArr,
									mFilterBankArr);
	}
	else{
		if(styleType==SpectralFilterBankStyle_Slaney){ // Slaney style

			__auditory_slaneyFilterBank(num,fftLength,samplate,isPseudo,
										normType,
										fArr,bArr,
										mFilterBankArr);
		}
		else if(styleType==SpectralFilterBankStyle_ETSI){ // ESTI style

			__auditory_estiFilterBank(num,fftLength,isPseudo,
									normType,
									fArr,bArr,
									mFilterBankArr);
		}
		else if(styleType==SpectralFilterBankStyle_Gammatone){ // gammatone style
			__auditory_gammatoneFilterBank(num,fftLength,samplate,isPseudo,
										normType,
										fArr,bArr,
										mFilterBankArr);
		}
		else{ // rect~gauss
			__auditory_windowFilterBank(num,fftLength,samplate,isPseudo,
										styleType,normType,
										fArr,bArr,
										mFilterBankArr);
		}
	}

	// 3. 处理freBand/binBand
	if(freBandArr){
		memcpy(freBandArr, fArr+offset, sizeof(float )*num);
	}
	
	if(binBandArr){
		memcpy(binBandArr, bArr+offset, sizeof(int )*num);
	}

	free(fArr);
	free(bArr);
}

// rect~guass 窗函数设计法
static void __auditory_windowFilterBank(int num,int fftLength,int samplate,int isPseudo,
									SpectralFilterBankStyleType winType,
									SpectralFilterBankNormalType normType,
									float *freBandArr,int *binBandArr,
									float *mFilterBankArr){
	int left=0;
	int cur=0;
	int right=0;

	int mLength=0;

	if(!isPseudo){
		mLength=fftLength/2+1;
	}
	else{
		mLength=fftLength;
	}

	// 1. all window freband
	if(winType==SpectralFilterBankStyle_Point){
		for(int i=1;i<num+1;i++){
			left=binBandArr[i-1];
			cur=binBandArr[i];
			right=binBandArr[i+1];

			mFilterBankArr[(i-1)*mLength+cur]=1.0;
		}
	}
	else if(winType==SpectralFilterBankStyle_Rect){
		for(int i=1;i<num+1;i++){
			left=binBandArr[i-1];
			cur=binBandArr[i];
			right=binBandArr[i+1];

			for(int j=left;j<=right;j++){
				mFilterBankArr[(i-1)*mLength+j]=1.0;
			}
		}
	}
	else{
		for(int i=1;i<num+1;i++){
			left=binBandArr[i-1];
			cur=binBandArr[i];
			right=binBandArr[i+1];

			if(cur>left){
				float *wArr=NULL;
				int _index=0;

				if(winType==SpectralFilterBankStyle_Hann){
					wArr=window_createHann(2*(cur-left)+1,0);
				}
				else if(winType==SpectralFilterBankStyle_Hamm){
					wArr=window_createHamm(2*(cur-left)+1,0);
				}
				else if(winType==SpectralFilterBankStyle_Blackman){
					wArr=window_createBlackman(2*(cur-left)+1,0);
				}
				else if(winType==SpectralFilterBankStyle_Bohman){
					wArr=window_createBohman(2*(cur-left)+1,0);
				}
				else if(winType==SpectralFilterBankStyle_Kaiser){
					wArr=window_createKaiser(2*(cur-left)+1,0,NULL);
				}
				else{ // gauss
					wArr=window_createGauss(2*(cur-left)+1,0,NULL);
				}

				for(int j=left,k=_index;j<=cur;j++,k++){ 
					mFilterBankArr[(i-1)*mLength+j]=wArr[k];
				}

				free(wArr);
			}

			if(right>cur){
				float *wArr=NULL;
				int _index=0;

				_index=(2*(right-cur)+1)/2+1;
				if(winType==SpectralFilterBankStyle_Hann){
					wArr=window_createHann(2*(right-cur)+1,0);
				}
				else if(winType==SpectralFilterBankStyle_Hamm){
					wArr=window_createHamm(2*(right-cur)+1,0);
				}
				else if(winType==SpectralFilterBankStyle_Blackman){
					wArr=window_createBlackman(2*(right-cur)+1,0);
				}
				else if(winType==SpectralFilterBankStyle_Bohman){
					wArr=window_createBohman(2*(right-cur)+1,0);
				}
				else if(winType==SpectralFilterBankStyle_Kaiser){
					wArr=window_createKaiser(2*(right-cur)+1,0,NULL);
				}
				else{ // gauss
					wArr=window_createGauss(2*(right-cur)+1,0,NULL);
				}
				
				for(int j=cur+1,k=_index;j<=right;j++,k++){ 
					mFilterBankArr[(i-1)*mLength+j]=wArr[k];
				}

				free(wArr);
			}
		}
	}

	// 2. 归一化
	if(normType==SpectralFilterBankNormal_Area||normType==SpectralFilterBankNormal_BandWidth){
		float *weightArr=NULL;

		weightArr=__vnew(num, NULL);
		if(normType==SpectralFilterBankNormal_Area){ // area
			__msum(mFilterBankArr, num, mLength, 1, weightArr);
			// mel/bark 计算一半
			// __vdiv_value(weightArr, 2, num, NULL);
		}
		else{ // bandwidth
			__vsub(freBandArr+2, freBandArr, num, weightArr);
			__vdiv_value(weightArr, 2, num, NULL);
		}

		__mdiv_vector(mFilterBankArr, weightArr,0, num, mLength, 1, NULL);

		free(weightArr);
	}
}

static void __auditory_linearFilterBank(int num,int fftLength,int samplate,int isPseudo,
										float *freBandArr,int *binBandArr,
										float *mFilterBankArr){
	int cur=0;
	int mLength=0;

	if(!isPseudo){
		mLength=fftLength/2+1;
	}
	else{
		mLength=fftLength;
	}

	// ???
	// for(int i=0;i<num;i++){
	// 	cur=binBandArr[i];
	// 	mFilterBankArr[i*mLength+cur]=1;
	// }

	// linear spec,binBandArr-1
	for(int i=1;i<num+1;i++){
		binBandArr[i]-=1;

		cur=binBandArr[i];
		mFilterBankArr[(i-1)*mLength+cur]=1;
	}
}

/***
	针对mel/bark ESTI-style 'bin'
	1. 三角频带
	2. 归一化
	filterBankArr=>matrix num*(fftLength/2+1)
****/
static void __auditory_estiFilterBank(int num,int fftLength,int isPseudo,
									SpectralFilterBankNormalType type,
									float *freBandArr,int *binBandArr,
									float *mFilterBankArr){
	int left=0;
	int cur=0;
	int right=0;

	int mLength=0;

	if(!isPseudo){
		mLength=fftLength/2+1;
	}
	else{
		mLength=fftLength;
	}

	// 1. 三角频带
	for(int i=1;i<num+1;i++){
		left=binBandArr[i-1];
		cur=binBandArr[i];
		right=binBandArr[i+1];

		if(cur>left){
			for(int j=left;j<=cur;j++){ // 三角上升 
				mFilterBankArr[(i-1)*mLength+j]=1.0*(j-left)/(cur-left);
			}
		}

		for(int j=cur+1;j<=right;j++){ // 三角下降
			mFilterBankArr[(i-1)*mLength+j]=1.0*(right-j)/(right-cur);
		}
	}

	// 2. norm
	if(type==SpectralFilterBankNormal_Area||type==SpectralFilterBankNormal_BandWidth){
		float *weightArr=NULL;

		weightArr=__vnew(num, NULL);
		if(type==SpectralFilterBankNormal_Area){ // area
			__msum(mFilterBankArr, num, mLength, 1, weightArr);
			// mel/bark 计算一半
			// __vdiv_value(weightArr, 2, num, NULL);
		}
		else{ // bandwidth
			__vsub(freBandArr+2, freBandArr, num, weightArr);
			__vdiv_value(weightArr, 2, num, NULL);
		}

		__mdiv_vector(mFilterBankArr, weightArr,0, num, mLength, 1, NULL);

		free(weightArr);
	}
}

/***
	针对mel/bark Slaney-style 'fre'
	1. 确定顶点
	2. 三角频带
	3. 归一化
	filterBankArr=>matrix num*(fftLength/2+1)
****/
static void __auditory_slaneyFilterBank(int num,int fftLength,int samplate,int isPseudo,
									SpectralFilterBankNormalType type,
									float *freBandArr,int *binBandArr,
									float *mFilterBankArr){
	float *fArr=NULL;
	float *wArr=NULL;

	int mLength=0;

	if(!isPseudo){
		mLength=fftLength/2+1;
	}
	else{
		mLength=fftLength;
	}

	wArr=__vnew(num+1, NULL);

	// 1. linear freArr; not samplate/2.0,fftLength/2+1 for stop overflow
	fArr=__vlinspace(0, samplate-samplate/(float )fftLength, fftLength, 0);
	// fArr=__vlinspace(0, samplate/2.0, fftLength/2+1, 0);

	// for(int i=0;i<num+2;i++){
	// 	for(int j=0;j<fftLength;j++){
	// 		if(fArr[j]>freBandArr[i]){
	// 			bArr[i]=j;
	// 			break;
	// 		}
	// 	}
	// }

	// 2. slaney
	__vsub(freBandArr+1, freBandArr, num+1, wArr);
	for(int i=0;i<num;i++){
		for(int j=binBandArr[i];j<=binBandArr[i+1]-1;j++){ 
			mFilterBankArr[i*mLength+j]=(fArr[j]-freBandArr[i])/wArr[i];
		}

		for(int j=binBandArr[i+1];j<=binBandArr[i+2]-1;j++){ 
			mFilterBankArr[i*mLength+j]=(freBandArr[i+2]-fArr[j])/wArr[i+1];
		}
	}

	// 3. norm
	if(type==SpectralFilterBankNormal_Area||type==SpectralFilterBankNormal_BandWidth){
		float *weightArr=NULL;

		weightArr=__vnew(num, NULL);
		if(type==SpectralFilterBankNormal_Area){ // area
			__msum(mFilterBankArr, num, mLength, 1, weightArr);
			// mel/bark 计算一半
			// __vdiv_value(weightArr, 2, num, NULL);
		}
		else{ // bandwidth
			__vsub(freBandArr+2, freBandArr, num, weightArr);
			__vdiv_value(weightArr, 2, num, NULL);
		}

		__mdiv_vector(mFilterBankArr, weightArr,0, num, mLength, 1, NULL);

		free(weightArr);
	}

	free(fArr);
	free(wArr);
}

/***
	针对erb
	1. freBand->coeff 频带计算滤波器系数
	2. coeff->bank 
	3. 归一化
	4. scale down/up 0&&fftLength/2两端不变 中间*2
****/
static void __auditory_gammatoneFilterBank(int num,int fftLength,int samplate,int isPseudo,
										SpectralFilterBankNormalType type,
										float *freBandArr,int *binBandArr,
										float *mFilterBankArr){
	float **cArrArr=NULL;

	int mLength=0;

	float *rArr=NULL;
	float *iArr=NULL;

	int isWhole=0;
	int len=0;

	int order=4;

	if(!isPseudo){
		mLength=fftLength/2+1;
	}
	else{
		mLength=fftLength;
	}
	
	if(!isWhole){
		len=fftLength/2+1;
	}
	else{
		len=fftLength;
	}

	// 1. freBand ->coeff 
	cArrArr=auditory_calGammatoneCoefficient(freBandArr,num,samplate);

	// 2. coeff->bank
	__vcnew(len, NULL, &rArr, &iArr);
	for(int i=0;i<num;i++){ // 32
		filterDesign_freqzSOS(cArrArr[i], order, 
							fftLength, samplate, isWhole,
							NULL,
							rArr, iArr, NULL);

		__vcabs(rArr, iArr, len, mFilterBankArr+i*len);
	}

	// 3. 归一化
	if(type==SpectralFilterBankNormal_Area||type==SpectralFilterBankNormal_BandWidth){
		float *weightArr=NULL;
		
		weightArr=__vnew(num, NULL);
		if(type==SpectralFilterBankNormal_Area){ // area
			if(!isWhole){ // 0~fftLength/2+1
				for(int i=0;i<num;i++){ // 0+fftLength/2
					weightArr[i]=mFilterBankArr[i*mLength]+mFilterBankArr[i*mLength+mLength-1];
					weightArr[i]+=__vsum(mFilterBankArr+(i*mLength+1), mLength-2)*2;
				}
			}
			else{
				__msum(mFilterBankArr, num, mLength, 1, weightArr);
			}
		}
		else{ // bandwidth
			for(int i=0;i<num;i++){
				weightArr[i]=1.019*24.7*(0.00437*freBandArr[i]+1);
			}

			__vdiv_value(weightArr, 2, num, NULL);
		}

		__mdiv_vector(mFilterBankArr, weightArr,0, num, mLength, 1, NULL);

		free(weightArr);
	}

	// 4. scale down/up
	for(int i=0;i<num;i++){
		for(int j=1;j<mLength-1;j++){
			mFilterBankArr[i*mLength+j]*=2;
		}
	}

	free(rArr);
	free(iArr);
}

// 计算band edge 针对mel/bark/erb/log bType 0 !slaney 1 slaney
static void __auditory_calBandEdge(int num,int fftLength,int samplate,
								float lowFre,float highFre,int isEdge,int bType,
								void *callback1,void *callback2,float ref,
								float **freBandArr,int **binBandArr){
	float *fArr=NULL;
	int *bArr=NULL;

	float low=0;
	float high=0;

	int det=0;

	UniFunc func1=NULL;
	UniFunc func2=NULL;

	UniFunc1 func3=NULL;
	UniFunc1 func4=NULL;

	if(!isEdge){ // ! gammatone
		det=2;
	}

	if(ref){
		func3=(UniFunc1 )callback1;
		func4=(UniFunc1 )callback2;

		low=func3(lowFre,ref);
		high=func3(highFre,ref);
	}
	else{
		func1=(UniFunc )callback1;
		func2=(UniFunc )callback2;

		low=func1(lowFre);
		high=func1(highFre);
	}

	// 1. mel/barkArr
	fArr=__vlinspace(low, high, num+det, 0);

	// 2. mel/barkArr=>freArr
	if(ref){
		__vmap1(fArr, num+det, func4,ref, NULL);
	}
	else{
		__vmap(fArr, num+det, func2, NULL);
	}

	if(freBandArr){
		*freBandArr=fArr;
	}

	// 3. freArr=>binArr vector???
	if(binBandArr){
		bArr=__vnewi(num+det, NULL);
		if(!bType){ // 非slaney
			for(int i=0;i<num+det;i++){
				bArr[i]=roundf(fftLength*fArr[i]/samplate);
			}
		}
		else{ // slaney
			float *_arr1=NULL;

			// not samplate/2.0,fftLength/2+1 for stop overflow
			_arr1=__vlinspace(0, samplate-samplate/(float )fftLength, fftLength, 0);
			for(int i=0;i<num+2;i++){
				for(int j=0;j<fftLength;j++){
					if(_arr1[j]>fArr[i]){
						bArr[i]=j;
						break;
					}
				}
			}

			free(_arr1);
		}

		*binBandArr=bArr;
	}

	if(!freBandArr){
		free(fArr);
	}
}

/***
	gammatone filter
		g(t)=(a*t^(n-1))*(e^(-2*PI*b*t))*cos(2*PI*fc*t+p)
		a= amp factor
		n= filter order,一般选用4阶(人类听觉系统模型)
		fc= center fre
		b= bandwidth ,1.019*fre2Erb(fc)
		p= phase factor
	1. 计算A11 A23 A13 A14 arr;A0 A2 B0 B1 B2
	2. 计算gain Arr共10个num向量
	3. 有10个num Arr 拼接num个4*6 matrix
****/
float **auditory_calGammatoneCoefficient(float *freBandArr,int length,int samplate){
	float **coefArrArr=NULL;

	float *erbArr=NULL; // 1.019*fre2Erb(fre)
	float *argArr=NULL; // 2*PI*fre*t
	float *vArr=NULL; // -t*e^(-(erbArr*t))

	float *cosArr=NULL; // cos(argArr)
	float *sinArr=NULL; // sin(argArr)

	// 复数相关
	float *cRealArr=NULL; // -2*t*e^(i*2*argArr)
	float *cImageArr=NULL;
	float *gRealArr=NULL; // 2*t*e^(i*argArr-erbArr*t)
	float *gImageArr=NULL;

	float *k11Arr=NULL;
	float *k12Arr=NULL;
	float *k13Arr=NULL;
	float *k14Arr=NULL;

	// BA gain系数相关
	float *a0Arr=NULL; // 1/samplate
	float *a2Arr=NULL; // 0
	float *b0Arr=NULL; // 1

	float *b1Arr=NULL;
	float *b2Arr=NULL;

	float *a11Arr=NULL;
	float *a12Arr=NULL;
	float *a13Arr=NULL;
	float *a14Arr=NULL;

	float *gainArr=NULL;

	float t=0;
	float v1=1;

	float pv=0;
	float nv=0;

	int nLen=0;
	int mLen=0;

	t=1.0/samplate;
	pv=sqrtf(3+powf(2, 1.5));
	nv=sqrtf(3-powf(2, 1.5));

	nLen=4;
	mLen=6;

	coefArrArr=(float **)calloc(length, sizeof(float *));
	for(int i=0;i<length;i++){
		coefArrArr[i]=__vnew(nLen*mLen, NULL);
	}

	erbArr=__vnew(length, NULL);
	argArr=__vnew(length, NULL);
	vArr=__vnew(length, NULL);

	cosArr=__vnew(length, NULL);
	sinArr=__vnew(length, NULL);

	cRealArr=__vnew(length, NULL);
	cImageArr=__vnew(length, NULL);
	gRealArr=__vnew(length, NULL);
	gImageArr=__vnew(length, NULL);

	k11Arr=__vnew(length, &t);
	k12Arr=__vnew(length, &t);
	k13Arr=__vnew(length, &t);
	k14Arr=__vnew(length, &t);

	a0Arr=__vnew(length, &t);
	a2Arr=__vnew(length, NULL);
	b0Arr=__vnew(length, &v1);

	b1Arr=__vnew(length, NULL);
	b2Arr=__vnew(length, NULL);

	a11Arr=__vnew(length, NULL);
	a12Arr=__vnew(length, NULL);
	a13Arr=__vnew(length, NULL);
	a14Arr=__vnew(length, NULL);

	gainArr=__vnew(length, NULL);

	// erbArr argArr
	for(int i=0;i<length;i++){
		erbArr[i]=(freBandArr[i]/9.26449+24.7)*2*M_PI*1.019; // fre=>erb space
		argArr[i]=freBandArr[i]*2*M_PI*t;
	}

	// vArr
	for(int i=0;i<length;i++){
		vArr[i]=-t*expf(-t*erbArr[i]);
	}

	// cosArr/sinArr
	for(int i=0;i<length;i++){
		cosArr[i]=cosf(argArr[i]);
		sinArr[i]=sinf(argArr[i]);
	}

	// real/image arr
	for(int i=0;i<length;i++){
		cRealArr[i]=cosf(4*M_PI*t*freBandArr[i]);
		cImageArr[i]=sinf(4*M_PI*t*freBandArr[i]);

		gRealArr[i]=2*t*expf(-erbArr[i]*t)*cos(2*M_PI*t*freBandArr[i]);
		gImageArr[i]=2*t*expf(-erbArr[i]*t)*sin(2*M_PI*t*freBandArr[i]);
	}

	// b1/b2 arr
	for(int i=0;i<length;i++){
		b1Arr[i]=-2*cosArr[i]/expf(erbArr[i]*t);
		b2Arr[i]=expf(-2*t*erbArr[i]);
	}

	// a11/a12/a13/a14
	for(int i=0;i<length;i++){
		k11Arr[i]=cosArr[i]+pv*sinArr[i];
		k12Arr[i]=cosArr[i]-pv*sinArr[i];
		k13Arr[i]=cosArr[i]+nv*sinArr[i];
		k14Arr[i]=cosArr[i]-nv*sinArr[i];

		a11Arr[i]=vArr[i]*k11Arr[i];
		a12Arr[i]=vArr[i]*k12Arr[i];
		a13Arr[i]=vArr[i]*k13Arr[i];
		a14Arr[i]=vArr[i]*k14Arr[i];
	}

	// gainArr
	for(int i=0;i<length;i++){
		float value=0;

		float r1=0,i1=0;
		float r2=0,i2=0;
		float r3=0,i3=0;
		float r4=0,i4=0;
		float r5=0,i5=0;

		r1=-2*t*cRealArr[i]+gRealArr[i]*k11Arr[i];
		i1=-2*t*cImageArr[i]+gImageArr[i]*k11Arr[i];

		r2=-2*t*cRealArr[i]+gRealArr[i]*k12Arr[i];
		i2=-2*t*cImageArr[i]+gImageArr[i]*k12Arr[i];

		r3=-2*t*cRealArr[i]+gRealArr[i]*k13Arr[i];
		i3=-2*t*cImageArr[i]+gImageArr[i]*k13Arr[i];

		r4=-2*t*cRealArr[i]+gRealArr[i]*k14Arr[i];
		i4=-2*t*cImageArr[i]+gImageArr[i]*k14Arr[i];

		r5=-2/expf(2*t*erbArr[i])-2*cRealArr[i]+2*(1+cRealArr[i])/expf(t*erbArr[i]);
		i5=-2*cImageArr[i]+2*cImageArr[i]/expf(t*erbArr[i]);

		value=sqrtf(r1*r1+i1*i1)*
				sqrtf(r2*r2+i2*i2)*
				sqrtf(r3*r3+i3*i3)*
				sqrtf(r4*r4+i4*i4)/((r5*r5+i5*i5)*(r5*r5+i5*i5));
		// value/=__complexPowM(r5,i5,4);

		gainArr[i]=value;
	}

	// 拼接length个n*m matraix
	for(int k=0;k<length;k++){
		for(int i=0;i<nLen;i++){ // nLength
			if(i==0){
				coefArrArr[k][0]=a0Arr[k]/gainArr[k];
				coefArrArr[k][1]=a11Arr[k]/gainArr[k];
				coefArrArr[k][2]=a2Arr[k]/gainArr[k];
				coefArrArr[k][3]=b0Arr[k];
				coefArrArr[k][4]=b1Arr[k];
				coefArrArr[k][5]=b2Arr[k];
			}
			else{
				float *arr=NULL;

				if(i==1){
					arr=a12Arr;
				}
				else if(i==2){
					arr=a13Arr;
				}
				else {
					arr=a14Arr;
				}

				coefArrArr[k][i*mLen+0]=a0Arr[k];
				coefArrArr[k][i*mLen+1]=arr[k];
				coefArrArr[k][i*mLen+2]=a2Arr[k];
				coefArrArr[k][i*mLen+3]=b0Arr[k];
				coefArrArr[k][i*mLen+4]=b1Arr[k];
				coefArrArr[k][i*mLen+5]=b2Arr[k];
			}
		}
	}

	free(erbArr);
	free(argArr);
	free(vArr);

	free(cosArr);
	free(sinArr);

	free(cRealArr);
	free(cImageArr);
	free(gRealArr);
	free(gImageArr);

	free(k11Arr);
	free(k12Arr);
	free(k13Arr);
	free(k14Arr);

	free(a0Arr);
	free(a2Arr);
	free(b0Arr);

	free(b1Arr);
	free(b2Arr);

	free(a11Arr);
	free(a12Arr);
	free(a13Arr);
	free(a14Arr);

	free(gainArr);

	return coefArrArr;
}

// isEdge 0 非gammatone high=low+num-1+2; 1 gammatone high=low+num-1
static void __reviseMidiFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3){
	float low=0;
	float high=0;

	int det=0;
	int offset=0;

	if(!isEdge){
		det=2;
		offset=1;
	}

	low=auditory_freToMidi(lowFre)-offset;
	high=low+num-1+det;

	*lowFre3=auditory_midiToFre(low);
	*highFre3=auditory_midiToFre(high);
}

static void __reviseLogFre(int num,float lowFre,float highFre,int binPerOctave,int isEdge,float *lowFre3,float *highFre3){
	float low=0;
	float high=0;

	int det=0;
	int offset=0;

	if(!isEdge){
		det=2;
		offset=1;
	}

	low=auditory_freToLog(lowFre,binPerOctave)-offset;
	high=low+num-1+det;

	*lowFre3=auditory_logToFre(low,binPerOctave);
	*highFre3=auditory_logToFre(high,binPerOctave);
}

static void __reviseLinearFre(int num,float lowFre,float highFre,float detFre,int isEdge,float *lowFre3,float *highFre3){
	float low=0;
	float high=0;

	int det=0;
	int offset=0;

	if(!isEdge){
		det=2;
		offset=1;
	}

	low=roundf(lowFre/detFre)-offset;
	high=low+num-1+det;

	*lowFre3=low*detFre;
	*highFre3=high*detFre;
}

static void __reviseLinspaceFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3){
	float detFre=0;

	if(!isEdge){
		detFre=(highFre-lowFre)/(num-1);

		*lowFre3=lowFre-detFre;
		*highFre3=highFre+detFre;
	}
	else{
		*lowFre3=lowFre;
		*highFre3=highFre;
	}
}

static void __reviseLogspaceFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3){
	float low=0;
	float high=0;

	float det=0;

	if(!isEdge){
		low=auditory_freToLogspace(lowFre);
		high=auditory_freToLogspace(highFre);

		det=(high-low)/(num-1);

		low=low-det;
		high=high+det;

		*lowFre3=auditory_logspaceToFre(low);
		*highFre3=auditory_logspaceToFre(high);
	}
	else{
		*lowFre3=lowFre;
		*highFre3=highFre;
	}
}

// linear scale
float auditory_freToLinear(float fre,float detFre){
	float value=0;

	value=roundf(fre/detFre);
	return value;
}

float auditory_linearToFre(float value,float detFre){
	float fre=0;

	fre=value*detFre;
	return fre;
}

// linspace scale
float auditory_freToLinspace(float fre){

	return fre;
}

float auditory_linspaceToFre(float value){

	return value;
}

// mel scale
// mel=2595*log10(1+fre/700)
float auditory_freToMel(float fre){
	float mel=0;

	mel=2595*log10f(1+fre/700);
	return mel;
}

// fre=700*(10^(mel/2595)-1)
float auditory_melToFre(float mel){
	float fre=0;

	fre=700*(powf(10, mel/2595)-1);
	return fre;
}

// bark scale 巴克
/***
	bark=26.81*fre/(1960+fre)-0.53
	bark=bark+0.15*(2-bark); bark<2
	bark=bark+0.22*(bark-20.1); bark>20.1
****/
float auditory_freToBark(float fre){
	float bark=0;

	bark=26.81*fre/(1960+fre)-0.53;
	if(bark<2){
		bark=bark+0.15*(2-bark);
	}
	else if(bark>20.1){
		bark=bark+0.22*(bark-20.1);
	}

	return bark;
}

/***
	bark=(bark-0.3)/0.85; bark<2
	bark=(bark+4.422)/1.22; bark>20.1
	fre=1960*(bark+0.53)/(26.28-bark);
****/
float auditory_barkToFre(float bark){
	float fre=0;

	if(bark<2){
		bark=(bark-0.3)/0.85;
	}
	else if(bark>20.1){
		bark=(bark+4.422)/1.22;
	}

	fre=1960*(bark+0.53)/(26.28-bark);

	return fre;
}

// erb scale 等效矩形带宽
/***
	erb=A*log10f(1+fre*0.004368)
	A=1000*logf(10)/(24.7*4.37) ~=21.3654
****/
float auditory_freToErb(float fre){
	float erb=0;
	float a=0;

	// a=1000*logf(10)/(24.7*4.37);
	a=21.3654;
	erb=a*log10f(1+fre*0.004368);

	return erb;
}

/***
	fre=(10^(erb/A)-1)/0.004368
	A=1000*logf(10)/(24.7*4.37) ~=21.3654
****/
float auditory_erbToFre(float erb){
	float fre=0;
	float a=0;

	// a=1000*logf(10)/(24.7*4.37);
	a=21.3654;
	fre=(powf(10, erb/a)-1)/0.004368;

	return fre;
}

// midi sacle
/***
	midi=12*log2(fre/440)+69
****/
float auditory_freToMidi(float fre){
	float midi=0;

	midi=roundf(12*log2(fre/440)+69);

	return midi;
}

float auditory_midiToFre(float midi){
	float fre=0;

	fre=powf(2,(midi-69)/12)*440;

	return fre;
}

float auditory_freToLog(float fre,float binPerOctave){
	float value=0;
	float n=0;

	n=binPerOctave/12;
	value=roundf(binPerOctave*log2(fre/440));

	return value;
}

float auditory_logToFre(float value,float binPerOctave){
	float fre=0;
	float n=0;

	n=binPerOctave/12;
	fre=pow(2,value/binPerOctave)*440;

	return fre;
}

// logspace scale
float auditory_freToLogspace(float fre){
	float value=0;

	value=log2(fre/440);
	return value;
}

float auditory_logspaceToFre(float value){
	float fre=0;

	fre=pow(2, value)*440;
	return fre;
}

void auditory_reviseLogFre(int num,float lowFre,float highFre,int binPerOctave,int isEdge,float *lowFre3,float *highFre3){

	__reviseLogFre(num,lowFre,highFre,binPerOctave,isEdge,lowFre3,highFre3);
}

void auditory_reviseLinearFre(int num,float lowFre,float highFre,float detFre,int isEdge,float *lowFre3,float *highFre3){

	__reviseLinearFre(num,lowFre,highFre,detFre,isEdge,lowFre3,highFre3);
}

void auditory_reviseLinspaceFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3){

	__reviseLinspaceFre(num, lowFre, highFre, isEdge, lowFre3, highFre3);
}

void auditory_reviseLogspaceFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3){

	__reviseLogspaceFre(num,lowFre, highFre, isEdge, lowFre3, highFre3);
}























```

---

### Archivo: `./src/filterbank/auditory_filterBank.h`

```


#ifndef AUDITORY_FILTERBANK_H
#define AUDITORY_FILTERBANK_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "../flux_base.h"

/***
	scale liespace/mel/bark/erb/log/logspace not include edge
	scale linear include edge
	style gammatone include edge
****/
void auditory_filterBank(int num,int fftLength,int samplate,int isPseudo,
						SpectralFilterBankScaleType scaleType,
						SpectralFilterBankStyleType styleType,
						SpectralFilterBankNormalType normType,
						float lowFre,float highFre,int binPerOctave,
						float *mFilterBankArr,
						float *freBandArr,
						int *binBandArr);

// linear scale
float auditory_freToLinear(float fre,float detFre);
float auditory_linearToFre(float value,float detFre);

// linspace scale
float auditory_freToLinspace(float fre);
float auditory_linspaceToFre(float value);

// mel scale
float auditory_freToMel(float fre);
float auditory_melToFre(float mel);

// bark scale 
float auditory_freToBark(float fre);
float auditory_barkToFre(float bark);

// erb scale -> equal rect bandwidth
float auditory_freToErb(float fre);
float auditory_erbToFre(float erb);

// midi sacle
float auditory_freToMidi(float fre);
float auditory_midiToFre(float midi);

// log sacle
float auditory_freToLog(float fre,float binPerOctave);
float auditory_logToFre(float value,float binPerOctave);

// logspace scale
float auditory_freToLogspace(float fre);
float auditory_logspaceToFre(float value);

void auditory_reviseLogFre(int num,float lowFre,float highFre,int binPerOctave,int isEdge,float *lowFre3,float *highFre3);
void auditory_reviseLinearFre(int num,float lowFre,float highFre,float detFre,int isEdge,float *lowFre3,float *highFre3);

void auditory_reviseLinspaceFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3);
void auditory_reviseLogspaceFre(int num,float lowFre,float highFre,int isEdge,float *lowFre3,float *highFre3);

// length -> 4*6 matrix
float **auditory_calGammatoneCoefficient(float *freBandArr,int length,int samplate);


#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/filterbank/cqt_filterBank.h`

```


#ifndef CQT_FILTERBANK_H
#define CQT_FILTERBANK_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>
#include "../flux_base.h"

// filterBank相关
void cqt_filterBank(int num,float *freBandArr,int samplate,
				int binPerOctave,SpectralFilterBankNormalType normType,WindowType *winType,
				float *factor,float *beta,float *thresh,
				float *lenArr,int fftLength,
				float *mRealFilterBankArr,float *mImageFilterBankArr);

void cqt_downFilterBank(int num,float *freBandArr,int samplate,
				int binPerOctave,SpectralFilterBankNormalType normType,WindowType *winType,
				float *factor,float *beta,float *thresh,
				float *lenArr,int fftLength,
				float *mRealFilterBankArr,float *mImageFilterBankArr);

float cqt_calQ(int binPerOctave,float factor);
float *cqt_calFreArr(float minFre,int num,int binPerOctave);

int cqt_calFFTLength(float minFre,int samplate,
				int binPerOctave,
				float *factor,float *beta);

void cqt_calLengthArr(int num,float *freBandArr,int samplate,
				int binPerOctave,
				float *factor,float *beta,
				float *lenArr);

#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/temporal_algorithm.c`

```
// clang 

#include <string.h>
#include <math.h>

#include "vector/flux_vector.h"
#include "vector/flux_vectorOp.h"
#include "vector/flux_complex.h"

#include "util/flux_util.h"

#include "dsp/flux_window.h"
#include "dsp/fft_algorithm.h"

#include "temporal_algorithm.h"

struct OpaqueTemporal{
	int frameLength;
	int slideLength;
	
	float *windowDataArr; // frameLength

	int timeLength;
	float *mDataArr; // timeLength*frameLength

	float *energyArr; // energy x(t)^2
	float *rmsArr; // rms sqrt(E/N)
	float *zcrArr; // zero-crossRate 

};

/***
	frameLength 2048
	slideLength 512
	windowType Hann
****/
int temporalObj_new(TemporalObj *temporalObj,
			 	int *frameLength,int *slideLength,WindowType *windowType){
	int status=0;

	int _frameLength=2048;
	int _slideLength=0;

	WindowType _windowType=Window_Hann;

	TemporalObj tmp=NULL;
	float *windowDataArr=NULL;

	tmp=*temporalObj=(TemporalObj )calloc(1, sizeof(struct OpaqueTemporal ));

	if(frameLength){
		if(*frameLength>0){
			_frameLength=*frameLength;
		}
	}

	_slideLength=_frameLength/4;
	if(slideLength){
		if(*slideLength>0){
			_slideLength=*slideLength;
		}
	}

	if(windowType){
		_windowType=*windowType;
	}

	windowDataArr=window_calFFTWindow(_windowType,_frameLength);

	tmp->frameLength=_frameLength;
	tmp->slideLength=_slideLength;

	tmp->windowDataArr=windowDataArr;

	return status;
}

int temporalObj_calTimeLength(TemporalObj temporalObj,int dataLength){
	int frameLength=0; 
	int slideLength=0;
	int timeLength=0;

	frameLength=temporalObj->frameLength;
	slideLength=temporalObj->slideLength;
	if(dataLength<frameLength){
		return 0;
	}

	timeLength=(dataLength-frameLength)/slideLength+1;
	return timeLength;
}

void temporalObj_temporal(TemporalObj temporalObj,float *dataArr,int dataLength){
	int frameLength=0; 
	int slideLength=0;
	int timeLength=0;

	float *windowDataArr=NULL; // frameLength

	float *energyArr=NULL; // energy x(t)^2
	float *rmsArr=NULL; // rms sqrt(E/N)
	float *zcrArr=NULL;

	float *mDataArr=NULL;

	frameLength=temporalObj->frameLength;
	slideLength=temporalObj->slideLength;
	if(dataLength<frameLength){
		return ;
	}

	timeLength=(dataLength-frameLength)/slideLength+1;
	if(temporalObj->timeLength<timeLength||
		temporalObj->timeLength>2*timeLength){

		free(temporalObj->energyArr);
		free(temporalObj->rmsArr);
		free(temporalObj->zcrArr);

		free(temporalObj->mDataArr);

		temporalObj->energyArr=__vnew(timeLength, NULL);
		temporalObj->rmsArr=__vnew(timeLength, NULL);
		temporalObj->zcrArr=__vnew(timeLength, NULL);

		temporalObj->mDataArr=__vnew(timeLength*frameLength, NULL);
	}

	windowDataArr=temporalObj->windowDataArr;

	energyArr=temporalObj->energyArr;
	rmsArr=temporalObj->rmsArr;
	zcrArr=temporalObj->zcrArr;

	mDataArr=temporalObj->mDataArr;

	// energy/rms/zcr
	for(int i=0;i<timeLength;i++){
		__vmul(dataArr+i*slideLength, windowDataArr, frameLength, mDataArr+i*frameLength);

		energyArr[i]=__venergy(mDataArr+i*frameLength, frameLength);
		rmsArr[i]=sqrtf(energyArr[i]/frameLength);
		zcrArr[i]=__vzcr(mDataArr+i*frameLength, frameLength);
	}

	temporalObj->timeLength=timeLength;
}

void temporalObj_getData(TemporalObj temporalObj,
						float **eArr,float **rArr,float **zArr,
						float **mDataArr){
	if(eArr){
		*eArr=temporalObj->energyArr;
	}

	if(rArr){
		*rArr=temporalObj->rmsArr;
	}

	if(zArr){
		*zArr=temporalObj->zcrArr;
	}

	if(mDataArr){
		*mDataArr=temporalObj->mDataArr;
	}
}

void temporalObj_ezr(TemporalObj temporalObj,float gamma,float *vArr3){
	float *energyArr=NULL; 
	float *zcrArr=NULL;

	int frameLength=0;
	int timeLength=0;

	float value1=0;
	float value2=0;

	energyArr=temporalObj->energyArr;
	zcrArr=temporalObj->zcrArr;

	frameLength=temporalObj->frameLength;
	timeLength=temporalObj->timeLength;
	for(int i=0;i<timeLength;i++){
		value1=log10f(1+energyArr[i]*gamma);
		value2=zcrArr[i]*frameLength+1;

		vArr3[i]=value1/value2;
	}
}

void temporal_free(TemporalObj temporalObj){

	if(temporalObj){
		free(temporalObj->windowDataArr);
		free(temporalObj->mDataArr);

		free(temporalObj->energyArr);
		free(temporalObj->rmsArr);
		free(temporalObj->zcrArr);

		free(temporalObj);
	}
}










```

---

### Archivo: `./src/flux_base.h`

```


#ifndef FLUX_BASE_H
#define FLUX_BASE_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

// window相关
typedef enum{
	Window_Rect=0, 
	Window_Hann,
	Window_Hamm,

	Window_Blackman,
	Window_Kaiser,

	Window_Bartlett,
	Window_Triang,

	Window_Flattop,
	Window_Gauss,

	Window_Blackman_Harris,
	Window_Blackman_Nuttall,
	Window_Bartlett_Hann,

	Window_Bohman,

	Window_Tukey, // tapered cosine

} WindowType;

typedef enum{
	FilterBand_LowPass=0, 
	FilterBand_HighPass,

	FilterBand_BandPass,
	FilterBand_BandStop, // Rejection

	// FilterBand_AllPass,

} FilterBandType;

// spectrum&&spectrogram 相关
typedef enum{
	SpectralData_Power=0,
	SpectralData_Mag,

} SpectralDataType;

typedef enum{
	SpectralFilterBankScale_Linear=0,
	SpectralFilterBankScale_Linspace,

	SpectralFilterBankScale_Mel, 
	SpectralFilterBankScale_Bark,
	SpectralFilterBankScale_Erb, 

	SpectralFilterBankScale_Octave, // similar Constant-Q
	SpectralFilterBankScale_Log,

	SpectralFilterBankScale_Deep, // similar Constant-Q 

	SpectralFilterBankScale_Chroma, // stft-chroma

	SpectralFilterBankScale_LogChroma, // similar cqt-chroma
	SpectralFilterBankScale_DeepChroma, // similar cqt-chroma

} SpectralFilterBankScaleType;

typedef enum{
	SpectralFilterBankStyle_Slaney=0, // Triang
	SpectralFilterBankStyle_ETSI, // Bartlett
	SpectralFilterBankStyle_Gammatone, // gammatone

	SpectralFilterBankStyle_Point,
	SpectralFilterBankStyle_Rect,
	
	SpectralFilterBankStyle_Hann, 
	SpectralFilterBankStyle_Hamm,

	SpectralFilterBankStyle_Blackman, 
	SpectralFilterBankStyle_Bohman,

	SpectralFilterBankStyle_Kaiser,
	SpectralFilterBankStyle_Gauss,

} SpectralFilterBankStyleType;

typedef enum{
	SpectralFilterBankNormal_None=0, // same hight

	SpectralFilterBankNormal_Area, // normal(same hight)/same area
	SpectralFilterBankNormal_BandWidth, 
	
} SpectralFilterBankNormalType;

typedef enum{
	SpectralNoveltyMethod_Sub=0, 

	SpectralNoveltyMethod_Entroy, 
	SpectralNoveltyMethod_KL, 
	SpectralNoveltyMethod_IS, 
	
} SpectralNoveltyMethodType;

typedef enum{
	SpectralNoveltyData_Value=0,
	SpectralNoveltyData_Number,
	
} SpectralNoveltyDataType;

typedef enum{
	ChromaDataNormal_None=0,

	ChromaDataNormal_Max, 
	ChromaDataNormal_Min, 

	ChromaDataNormal_P2, 
	ChromaDataNormal_P1, 
	
} ChromaDataNormalType;

typedef enum{
	CepstralRectify_Log=0,
	CepstralRectify_CubicRoot,

} CepstralRectifyType;

typedef enum{
	CepstralEnergy_Replace=0,
	CepstralEnergy_Append,
	CepstralEnergy_Ignore,

} CepstralEnergyType;

typedef enum{
	PaddingPosition_Center=0,
	PaddingPosition_Right,
	PaddingPosition_Left,

} PaddingPositionType;

typedef enum{
	PaddingMode_Constant=0,
	PaddingMode_Reflect,
	PaddingMode_Wrap, // repeat

} PaddingModeType;

typedef enum{
	WaveletContinue_Morse=0,
	WaveletContinue_Morlet,
	WaveletContinue_Bump,

	WaveletContinue_Paul, 
	WaveletContinue_DOG, // DOG
	WaveletContinue_Mexican, // DOG order=2

	WaveletContinue_Hermit,
	WaveletContinue_Ricker,
	
} WaveletContinueType;

typedef enum{
	WaveletDiscrete_Haar=0,
	WaveletDiscrete_Db, // 2~10/20/30/40
	WaveletDiscrete_Sym, // 2~10/20/30
	WaveletDiscrete_Coif, // 1~5

	WaveletDiscrete_FK, // 4/6/8/14/18/22

	/***
		1.1/1.3/1.5
		2.2/2.4/2.6/2.8
		3.1/3.3/3.5/3.7/3.9
		4.4/5.5/6.8
	****/
	WaveletDiscrete_Bior, 
	WaveletDiscrete_DMey,

} WaveletDiscreteType;



#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/cqt_algorithm.c`

```
// clang -g -c 

#include <string.h>
#include <math.h>

#include "vector/flux_vector.h"
#include "vector/flux_complex.h"

#include "util/flux_util.h"

#include "dsp/fft_algorithm.h"
#include "dsp/dct_algorithm.h"
#include "dsp/resample_algorithm.h"

#include "filterbank/cqt_filterBank.h"
#include "filterbank/chroma_filterBank.h"

#include "stft_algorithm.h"
#include "cqt_algorithm.h"

struct OpaqueCQT{
	int isContinue; // 针对cqt 非stft/resample 
	int vFlag; // vqt标志

	STFTObj stftObj;
	ResampleObj resampleObj;

	int fftLength; // fftLength,timeLength,num
	int timeLength; // cqt timeLength isContinue 0 ==stft timeLength
	int stftTimeLength;

	// filterBank相关
	int num;
	int octaveNum;
	int binPerOctave;

	float *mRealFilterBankArr; // num*(fftLength/2+1) -> binPerOctave*(fftLength/2+1)
	float *mImageFilterBankArr;

	float *freBandArr; // num
	float *lenArr; // binPerOctave

	float *sLenArr; // 针对 num sqrt
	float *dLenArr; // 针对 octaveNum sqrt

	int samplate;
	WindowType windowType;
	SpectralFilterBankNormalType normType;
	int isScale;

	float minFre; // C1 32.703196
	int chromaNum; // 默认12
	float *mChromaFilterBank; // chromaNum*num 
	float *mSArr; // timeLength*num

	// continue相关数据
	float *tailDataArr;
	int tailDataLength;

	float *validDataArr;
	int validDataLength;

	// stft相关
	float *mRealArr1; // stft r,i(timeLength*fftLength) -> power r(timeLength*(fftLength/2+1)) 
	float *mImageArr1;

	float *mRealArr2; // timeLength*binPerOctave
	float *mImageArr2;

	int radix2Exp; // stft
	int slideLength;

	// dct相关
	FFTObj fftObj; // dct加速
	DCTObj dctObj; // 直接矩阵

	// deconv相关
	FFTObj devFFTObj;
	int devFFTLength;

	float *devDataArr; // spectral mag&fft mag

	float *devRealArr1; // fft
	float *devImageArr1;

	float *devRealArr2; // ifft
	float *devImageArr2;

	int isDebug;
};

static void _cqtObj_dealFilterBank(CQTObj cqtObj,int num,float minFre,int samplate,
								int binPerOctave,SpectralFilterBankNormalType normType,WindowType winType,
								float factor,float beta,float thresh,int vFlag);
static void _cqtObj_dealStft(CQTObj cqtObj,int fftLength,int slideLength,int isContinue);
static void _cqtObj_dealResample(CQTObj cqtObj);

static void _cqtObj_dealDeconv(CQTObj cqtObj);

static void _cqtObj_dealDCT(CQTObj cqtObj,int num);

// 处理tail/cur Data
static int _cqtObj_dealData(CQTObj cqtObj,float *dataArr,int dataLength);
static void _cqtObj_cqt(CQTObj cqtObj,float *dataArr,int dataLength,float *mRealArr,float *mImageArr);

static void __calTimeAndTailLen(int dataLength,int fftLength,int slideLength,int isContinue,int *timeLength,int *tailLength);

static int _calRadix2(int length);

int cqtObj_new(CQTObj *cqtObj,int num,int samplate,float minFre,int *isContinue){
	int status=0;

	status=cqtObj_newWith(cqtObj,num,
						&samplate,&minFre,NULL,
						NULL,NULL,NULL,
						NULL,NULL,isContinue,
						NULL,NULL);

	return status;
}

// 7*binPerOctave --> binPerOctave-fftLength 12-512/24-1024/36-1024/48-2048
int cqtObj_newWith(CQTObj *cqtObj,int num,
				int *samplate,float *minFre,int *binPerOctave,
				float *factor,float *beta,float *thresh,
				WindowType *windowType,int *slideLength,int *isContinue,
				SpectralFilterBankNormalType *normalType,int *isScale){
	int status=0;
	CQTObj cqt=NULL;

	int _samplate=32000;
	float _minFre=32.703196; // C1
	int _binPerOctave=12;

	float _factor=1;
	float _beta=0;
	float _thresh=0.01; // paper 0.0054
	
	int _slideLength=0;
	int _isContinue=0;
	int vFlag=0;

	float *tailDataArr=NULL;

	WindowType _windowType=Window_Hann;
	SpectralFilterBankNormalType _normalType=SpectralFilterBankNormal_None;

	int _isScale=1;

	cqt=*cqtObj=(CQTObj )calloc(1, sizeof(struct OpaqueCQT ));

	if(binPerOctave){
		if(*binPerOctave>0){
			_binPerOctave=*binPerOctave;
		}
	}

	if(_binPerOctave%12!=0){
		printf("binPerOctave is error\n");
		return -1;
	}

	if(num<_binPerOctave||num%_binPerOctave!=0){
		printf("num is error\n");
		return -1;
	}

	if(samplate){
		if(*samplate>0){
			_samplate=*samplate;
		}
	}

	if(minFre){
		if(*minFre>0){
			_minFre=*minFre;
		}
	}

	if(factor){
		if(*factor>0){
			_factor=*factor;
		}
	}

	if(beta){
		if(*beta>0){
			_beta=*beta;
		}
		
		if(_beta!=0){
			vFlag=1;
		}
	}

	if(thresh){
		if(*thresh>0){
			_thresh=*thresh;
		}
	}

	if(windowType){
		_windowType=*windowType;
	}

	if(slideLength){
		if(*slideLength>0){
			_slideLength=*slideLength;
		}
	}

	if(isContinue){
		_isContinue=*isContinue;
	}

	if(normalType){
		_normalType=*normalType;
	}

	if(isScale){
		_isScale=*isScale;
	}

	_cqtObj_dealFilterBank(cqt,num,_minFre,_samplate,
						_binPerOctave,_normalType,_windowType,
						_factor,_beta,_thresh,vFlag);

	if(_slideLength<=0){ // 支持非overlap >fftLength
		_slideLength=cqt->fftLength/4;
	}

	tailDataArr=(float *)calloc(cqt->fftLength, sizeof(float ));

	_cqtObj_dealStft(cqt,cqt->fftLength,_slideLength,_isContinue);
	_cqtObj_dealResample(cqt);
	_cqtObj_dealDCT(cqt,num);

	cqt->tailDataArr=tailDataArr;

	cqt->isScale=_isScale;
	cqt->isContinue=_isContinue;
	cqt->vFlag=vFlag;

	cqt->minFre=_minFre;

	return status;
}

static void _cqtObj_dealDCT(CQTObj cqtObj,int num){
	FFTObj fftObj=NULL;
	DCTObj dctObj=NULL;
	int r=0;

	r=_calRadix2(num);
	if(r){ // dct加速
		fftObj_new(&fftObj, r);
	}
	else{ // 直接dct
		dctObj_new(&dctObj, num,NULL);
	}

	cqtObj->fftObj=fftObj;
	cqtObj->dctObj=dctObj;
}

int cqtObj_calTimeLength(CQTObj cqtObj,int dataLength){
	int fftLength=0; 
	int slideLength=0;
	int tailDataLength=0;

	int isContinue=0;

	int timeLength=0;

	fftLength=cqtObj->fftLength;
	slideLength=cqtObj->slideLength;
	tailDataLength=cqtObj->tailDataLength;

	isContinue=cqtObj->isContinue;

	if(isContinue){
		dataLength+=tailDataLength; // outTimeLength

		if(dataLength<fftLength){
			return 0;
		}

		timeLength=(dataLength-fftLength)/slideLength+1;
	}
	else{
		if(dataLength<=0){
			return 0;
		}

		timeLength=dataLength/slideLength+1;
	}

	return timeLength;
}

/***
	isContinue =1
		dataLength>=fftLength
		t=(dataLength-fftLength)/slideLength+1 
	isContinue =0
		dataLength>0
		t=(dataLength+fftLength-fftLength)/slideLength+1 ;padding fftLength
****/
static void __calTimeAndTailLen(int dataLength,int fftLength,int slideLength,int isContinue,int *timeLength,int *tailLength){
	int timeLen=0;
	int tailLen=0;

	if(isContinue){ // 连续
		timeLen=(dataLength-fftLength)/slideLength+1;
		tailLen=(dataLength-fftLength)%slideLength+(fftLength-slideLength);
	}
	else{
		timeLen=dataLength/slideLength+1;
		// if(timeLen>1){
		// 	tailLen=dataLength%slideLength;
		// }
	}

	if(timeLength){
		*timeLength=timeLen;
	}

	if(tailLength){
		*tailLength=tailLen;
	}
}

int cqtObj_getFFTLength(CQTObj cqtObj){
	int length=0;

	length=cqtObj->fftLength;
	return length;
}

float *cqtObj_getFreBandArr(CQTObj cqtObj){

	return cqtObj->freBandArr;
}

// isContinue 1 时处理tail/cur Data 
static int _cqtObj_dealData(CQTObj cqtObj,float *dataArr,int dataLength){
	int status=1;

	int isContinue=0;

	int fftLength=0; // fftLength,timeLength,num
	int timeLength=0;

	int slideLength=0;

	float *tailDataArr=NULL;
	int tailDataLength=0;

	float *validDataArr=NULL;
	int validDataLength=0;

	int timeLen=0;
	int tailLen=0;

	int totalLength=0;

	isContinue=cqtObj->isContinue;

	fftLength=cqtObj->fftLength;
	timeLength=cqtObj->timeLength;

	slideLength=cqtObj->slideLength;

	tailDataArr=cqtObj->tailDataArr;
	tailDataLength=cqtObj->tailDataLength;

	validDataArr=cqtObj->validDataArr;
	validDataLength=cqtObj->validDataLength;

	if(isContinue){ 
		totalLength=tailDataLength+dataLength;

		if(totalLength<fftLength){
			tailLen=totalLength;
			status=0;
		}

		if(status){
			__calTimeAndTailLen(totalLength, fftLength, slideLength,isContinue, &timeLen, &tailLen);
		}
	}
	else{
		totalLength=dataLength;
		__calTimeAndTailLen(totalLength, fftLength, slideLength,isContinue, &timeLen, &tailLen);
	}

	if(status){
		if(totalLength>validDataLength||
			validDataLength>2*totalLength){

			free(validDataArr);
			validDataArr=(float *)calloc(totalLength+fftLength, sizeof(float ));
		}

		validDataLength=0;
		if(isContinue&&tailDataLength<0){
			memcpy(validDataArr, dataArr-tailDataLength, (dataLength+tailDataLength)*sizeof(float ));
			validDataLength=(dataLength+tailDataLength);
		}
		else{
			if(isContinue&&tailDataLength>0){ // 连续且存在尾数据
				memcpy(validDataArr, tailDataArr, tailDataLength*sizeof(float ));
				validDataLength+=tailDataLength;
			}

			memcpy(validDataArr+validDataLength, dataArr, dataLength*sizeof(float ));
			validDataLength+=dataLength;
		}
		
		// 2. tailDataArr相关
		tailDataLength=0;
		if(isContinue){
			if(tailLen>0){
				memcpy(tailDataArr, validDataArr+(validDataLength-tailLen), tailLen*sizeof(float ));
			}

			tailDataLength=tailLen;
		}
	}
	else{
		// 2. tailDataArr相关
		if(isContinue){ 
			if(tailLen>0){
				if(tailDataLength>=0){
					memcpy(tailDataArr+tailDataLength,dataArr,dataLength*sizeof(float ));
				}
				else{
					memcpy(tailDataArr,dataArr-tailDataLength,(dataLength+tailDataLength)*sizeof(float ));
				}
			}
			
			tailDataLength=tailLen;
		}
		else{
			tailDataLength=0;
		}
	}

	cqtObj->tailDataLength=tailDataLength;

	cqtObj->validDataArr=validDataArr;
	cqtObj->validDataLength=validDataLength;

	cqtObj->timeLength=timeLen;
	return status;
}

void cqtObj_setScale(CQTObj cqtObj,int flag){

	cqtObj->isScale=flag;
}

void cqtObj_cqt(CQTObj cqtObj,float *dataArr,int dataLength,float *mRealArr3,float *mImageArr3){
	int status=0;

	if(!dataArr||dataLength<=0){
		return;
	}

	// 1. 处理相关数据
	status=_cqtObj_dealData(cqtObj,dataArr,dataLength);
	if(!status){
		return;
	}
	
	// 2. cqt
	_cqtObj_cqt(cqtObj,cqtObj->validDataArr,cqtObj->validDataLength,mRealArr3,mImageArr3);
}

/***
	cqt->chroma
	num(84) --> binPerOctave(12) --> chromaNum
****/
void cqtObj_chroma(CQTObj cqtObj,int *chromaNum,SpectralDataType *dataType,ChromaDataNormalType *normType,
				float *mRealArr1,float *mImageArr1,
				float *mDataArr3){
	int _chromaNum=12;

	SpectralDataType _dataType=SpectralData_Power;
	ChromaDataNormalType _normType=ChromaDataNormal_Max;

	int timeLength=0;

	int num=0;
	int binPerOctave=0;

	float *mChromaFilterBank=NULL;
	float *mSArr=NULL;

	float p1=1;
	int type1=0;

	if(chromaNum){
		_chromaNum=*chromaNum;
	}

	if(dataType){
		// if(*dataType<SpectralData_DB){
		// 	_dataType=*dataType;
		// }
		_dataType=*dataType;
	}

	if(normType){
		_normType=*normType;
	}

	timeLength=cqtObj->timeLength;

	num=cqtObj->num;
	binPerOctave=cqtObj->binPerOctave;

	if(_chromaNum>binPerOctave||binPerOctave%_chromaNum!=0){
		printf("chromaNum and binPerOctave not map!!!");
		return;
	}

	mChromaFilterBank=cqtObj->mChromaFilterBank;
	mSArr=cqtObj->mSArr;
	if(_chromaNum!=cqtObj->chromaNum){
		free(mSArr);
		free(mChromaFilterBank);
		
		mSArr=__vnew(timeLength*num, NULL);
		mChromaFilterBank=__vnew(_chromaNum*num, NULL);
		
		chroma_cqtFilterBank(_chromaNum,num,binPerOctave,
							&cqtObj->minFre,
							mChromaFilterBank);
	}

	for(int i=0;i<timeLength;i++){
		for(int j=0;j<num;j++){
			float _value=0;

			_value=mRealArr1[i*num+j]*mRealArr1[i*num+j]+mImageArr1[i*num+j]*mImageArr1[i*num+j];
			if(_dataType==SpectralData_Mag){
				_value=sqrtf(_value);
			}

			mSArr[i*num+j]=_value;
		}
	}

	__mdot1(mSArr,mChromaFilterBank,
		timeLength,num,
		_chromaNum,num,
		mDataArr3);

	// for(int i=0;i<timeLength;i++){
	// 	for(int j=0;j<num;j++){
	// 		float _value=0;

	// 		_value=mRealArr1[i*num+j]*mRealArr1[i*num+j]+mImageArr1[i*num+j]*mImageArr1[i*num+j];
	// 		if(_dataType==SpectralData_Mag){
	// 			_value=sqrtf(_value);
	// 		}

	// 		// sum == chromaMatrix.dot(S)
	// 		mDataArr3[i*binPerOctave+j%binPerOctave]+=_value;
	// 		// if(mDataArr3[i*binPerOctave+j%binPerOctave]<_value){ // max
	// 		// 	mDataArr3[i*binPerOctave+j%binPerOctave]=_value;
	// 		// }
	// 	}
	// }

	if(_normType!=ChromaDataNormal_None){
		if(_normType==ChromaDataNormal_Max){
			type1=1;
		}
		else if(_normType==ChromaDataNormal_Min){
			type1=2;
		}
		else{
			type1=0;
			if(_normType==ChromaDataNormal_P2){
				p1=2;
			}
		}

		__mnormalize(mDataArr3,timeLength,_chromaNum,1,type1,p1,mDataArr3);
	}

	cqtObj->chromaNum=_chromaNum;
	cqtObj->mChromaFilterBank=mChromaFilterBank;
	cqtObj->mSArr=mSArr;
}

void cqtObj_cqcc(CQTObj cqtObj,float *mDataArr1,int mLength,CepstralRectifyType *rectifyType,float *mDataArr2){
	FFTObj fftObj=NULL;
	DCTObj dctObj=NULL;

	CepstralRectifyType recType=CepstralRectify_Log;

	int num=0;
	int timeLength=0;

	float *mRealArr=NULL; 
	float *mImageArr=NULL;

	num=cqtObj->num;
	timeLength=cqtObj->timeLength;

	mRealArr=cqtObj->mRealArr1;
	mImageArr=cqtObj->mImageArr1;

	fftObj=cqtObj->fftObj;
	dctObj=cqtObj->dctObj;

	if(mLength>num){
		return;
	}

	if(rectifyType){
		recType=*rectifyType;
	}

	if(recType==CepstralRectify_CubicRoot){
		for(int i=0;i<timeLength*num;i++){
			mRealArr[i]=powf(mDataArr1[i], 1.0/3);
		}
	}
	else { // log
		for(int i=0;i<timeLength*num;i++){
			float _value=0;

			_value=mDataArr1[i];
			if(_value<1e-8){
				_value=1e-8;
			}

			mRealArr[i]=log10f(_value); // matlab canonic
		}
	}

	for(int i=0;i<timeLength;i++){
		if(fftObj){
			fftObj_dct(fftObj, mRealArr+i*num, mImageArr+i*num, 1);
		}
		else{
			dctObj_dct(dctObj, mRealArr+i*num,1,mImageArr+i*num);
		}
	}

	for(int i=0;i<timeLength;i++){
		for(int j=0;j<mLength;j++){
			mDataArr2[i*mLength+j]=mImageArr[i*num+j];
		}
	}
}

void cqtObj_cqhc(CQTObj cqtObj,float *mDataArr1,int hcNum,float *mDataArr2){
	int timeLength=0;
	int num=0;
	
	FFTObj devFFTObj=NULL;
	int devFFTLength=0;

	float *devDataArr=NULL; // cqt mag&fft mag

	float *devRealArr1=NULL; // fft
	float *devImageArr1=NULL;

	float *devRealArr2=NULL; // ifft
	float *devImageArr2=NULL;

	timeLength=cqtObj->timeLength;
	num=cqtObj->num;

	// 1. 处理缓存
	_cqtObj_dealDeconv(cqtObj);
	devFFTObj=cqtObj->devFFTObj;
	devFFTLength=cqtObj->devFFTLength;

	devDataArr=cqtObj->devDataArr;

	devRealArr1=cqtObj->devRealArr1;
	devImageArr1=cqtObj->devImageArr1;

	devRealArr2=cqtObj->devRealArr2;
	devImageArr2=cqtObj->devImageArr2;

	for(int i=0;i<timeLength;i++){
		// 2. fft&power
		memset(devDataArr, 0, sizeof(float )*devFFTLength);
		memcpy(devDataArr, mDataArr1+i*num, sizeof(float )*num);

		fftObj_fft(devFFTObj, devDataArr, NULL, devRealArr1, devImageArr1);
		__vcabs(devRealArr1, devImageArr1, devFFTLength, devDataArr);

		// 3. timbre --> real(ifft)
		fftObj_ifft(devFFTObj, devDataArr, NULL, devRealArr2, devImageArr2);
		// memcpy(mDataArr2+i*num, devRealArr2, sizeof(float )*num);

		// 4. cqhc
		for(int j=0;j<hcNum;j++){
			int _index=0;

			_index=roundf(cqtObj->binPerOctave*log2f(j+1));
			mDataArr2[i*hcNum+j]=devRealArr2[_index];
		}
	}
}

/***
	mDataArr1 mag/power
	mDataArr2 timbre(formant)
	mDataArr3 pitch
****/
void cqtObj_deconv(CQTObj cqtObj,float *mDataArr1,float *mDataArr2,float *mDataArr3){
	int timeLength=0;
	int num=0;
	
	FFTObj devFFTObj=NULL;
	int devFFTLength=0;

	float *devDataArr=NULL; // cqt mag&fft mag

	float *devRealArr1=NULL; // fft
	float *devImageArr1=NULL;

	float *devRealArr2=NULL; // ifft
	float *devImageArr2=NULL;

	timeLength=cqtObj->timeLength;
	num=cqtObj->num;

	// 1. 处理缓存
	_cqtObj_dealDeconv(cqtObj);
	devFFTObj=cqtObj->devFFTObj;
	devFFTLength=cqtObj->devFFTLength;

	devDataArr=cqtObj->devDataArr;

	devRealArr1=cqtObj->devRealArr1;
	devImageArr1=cqtObj->devImageArr1;

	devRealArr2=cqtObj->devRealArr2;
	devImageArr2=cqtObj->devImageArr2;

	for(int i=0;i<timeLength;i++){
		// 2. fft&mag
		memset(devDataArr, 0, sizeof(float )*devFFTLength);
		memcpy(devDataArr, mDataArr1+i*num, sizeof(float )*num);

		fftObj_fft(devFFTObj, devDataArr, NULL, devRealArr1, devImageArr1);
		__vcabs(devRealArr1, devImageArr1, devFFTLength, devDataArr);

		// 3. timbre --> real(ifft)
		fftObj_ifft(devFFTObj, devDataArr, NULL, devRealArr2, devImageArr2);
		memcpy(mDataArr2+i*num, devRealArr2, sizeof(float )*num);

		// 4. pitch --> real(ifft)
		for(int j=0;j<devFFTLength;j++){
			float _value=0;

			_value=devDataArr[j];
			if(_value<1e-16){
				_value=1e-16;
			}

			// devRealArr1[j]/=(devDataArr[j]+1e-16);
			// devImageArr1[j]/=(devDataArr[j]+1e-16);
			devRealArr1[j]/=_value;
			devImageArr1[j]/=_value;
		}

		fftObj_ifft(devFFTObj, devRealArr1, devImageArr1, devRealArr2, devImageArr2);
		memcpy(mDataArr3+i*num, devRealArr2, sizeof(float )*num);
	}
}

static void _cqtObj_dealDeconv(CQTObj cqtObj){
	FFTObj devFFTObj=NULL;
	int devFFTLength=0;

	float *devDataArr=NULL;

	float *devRealArr1=NULL;
	float *devImageArr1=NULL;

	float *devRealArr2=NULL;
	float *devImageArr2=NULL;

	int num=0;
	int radix2Exp=0;

	num=cqtObj->num;
	devFFTLength=util_ceilPowerTwo(2*num);
	if(devFFTLength!=cqtObj->devFFTLength){
		devFFTObj=cqtObj->devFFTObj;

		devDataArr=cqtObj->devDataArr;

		devRealArr1=cqtObj->devRealArr1;
		devImageArr1=cqtObj->devImageArr1;

		devRealArr2=cqtObj->devRealArr2;
		devImageArr2=cqtObj->devImageArr2;

		fftObj_free(devFFTObj);

		free(devDataArr);

		free(devRealArr1);
		free(devImageArr1);

		free(devRealArr2);
		free(devImageArr2);

		radix2Exp=util_powerTwoBit(devFFTLength);
		fftObj_new(&devFFTObj, radix2Exp);

		devDataArr=__vnew(devFFTLength, NULL);

		devRealArr1=__vnew(devFFTLength, NULL);
		devImageArr1=__vnew(devFFTLength, NULL);

		devRealArr2=__vnew(devFFTLength, NULL);
		devImageArr2=__vnew(devFFTLength, NULL);

		cqtObj->devFFTObj=devFFTObj;
		cqtObj->devFFTLength=devFFTLength;

		cqtObj->devDataArr=devDataArr;

		cqtObj->devRealArr1=devRealArr1;
		cqtObj->devImageArr1=devImageArr1;

		cqtObj->devRealArr2=devRealArr2;
		cqtObj->devImageArr2=devImageArr2;
	}
}

static void _cqtObj_cqt(CQTObj cqtObj,float *dataArr,int dataLength,float *mRealArr3,float *mImageArr3){
	STFTObj stftObj=NULL;
	ResampleObj resampleObj=NULL;

	int fftLength=0; // fftLength,timeLength,num
	int timeLength=0;
	int stftTimeLength=0;

	int slideLength=0;

	int num=0;
	int binPerOctave=0;
	int octaveNum=0;

	float *mRealFilterBankArr=NULL; // num*(fftLength/2+1)
	float *mImageFilterBankArr=NULL;

	float *freBandArr=NULL; // num
	float *lenArr=NULL;

	float *sLenArr=NULL;
	float *dLenArr=NULL;
	
	float *mRealArr1=NULL;
	float *mImageArr1=NULL;

	float *mRealArr2=NULL;
	float *mImageArr2=NULL;

	int normType=0;

	float *preDataArr=NULL;
	float *curDataArr=NULL;

	int preDataLength=0;
	int curDataLength=0;

	int index1=0;
	int vFlag=0;

	int isContinue=0;

	vFlag=cqtObj->vFlag;
	isContinue=cqtObj->isContinue;

	stftObj=cqtObj->stftObj;
	resampleObj=cqtObj->resampleObj;

	fftLength=cqtObj->fftLength;
	
	num=cqtObj->num;
	binPerOctave=cqtObj->binPerOctave;
	octaveNum=cqtObj->octaveNum;

	mRealFilterBankArr=cqtObj->mRealFilterBankArr; // num*(fftLength/2+1)
	mImageFilterBankArr=cqtObj->mImageFilterBankArr;

	freBandArr=cqtObj->freBandArr;
	lenArr=cqtObj->lenArr;

	sLenArr=cqtObj->sLenArr;
	dLenArr=cqtObj->dLenArr;

	mRealArr1=cqtObj->mRealArr1; // timeLength*fftLength
	mImageArr1=cqtObj->mImageArr1;

	mRealArr2=cqtObj->mRealArr2; // timeLength*binPerOctave
	mImageArr2=cqtObj->mImageArr2;

	normType=cqtObj->normType;

	preDataArr=__vnew(dataLength, NULL);
	curDataArr=__vnew(dataLength, NULL);
	preDataLength=dataLength;

	slideLength=cqtObj->slideLength;

	stftTimeLength=dataLength/slideLength+1;
	if(!isContinue){
		timeLength=stftTimeLength;
	}
	else{
		timeLength=(dataLength-fftLength)/slideLength+1;
	}

	if(cqtObj->stftTimeLength<stftTimeLength||
		cqtObj->stftTimeLength>stftTimeLength*2){ // 更新缓存
		free(mRealArr1);
		free(mImageArr1);

		free(mRealArr2);
		free(mImageArr2);

		/***
			down stft timeLength可能比top stft timeLength多1
			cqt timeLength以top stft timeLength为准
			内存尺度 timeLength*fftLength => (timeLength+1)*fftLength
		****/
		mRealArr1=__vnew((stftTimeLength+1)*fftLength, NULL);
		mImageArr1=__vnew((stftTimeLength+1)*fftLength, NULL);

		mRealArr2=__vnew((stftTimeLength+1)*binPerOctave, NULL);
		mImageArr2=__vnew((stftTimeLength+1)*binPerOctave, NULL);
	}

	// 1. top octave
	stftObj_setSlideLength(stftObj, slideLength);
	stftObj_stft(stftObj,dataArr,dataLength,mRealArr1,mImageArr1);

	// t*fftLength => t*(fftLength/2+1)
	for(int i=1;i<timeLength;i++){
		for(int j=0;j<(fftLength/2+1);j++){
			mRealArr1[i*(fftLength/2+1)+j]=mRealArr1[i*fftLength+j];
			mImageArr1[i*(fftLength/2+1)+j]=mImageArr1[i*fftLength+j];
		}
	}

	// S.dot(filterBank) t*(fftLength/2+1) @ num*(fftLength/2+1)
	if(vFlag){ // vqt num
		index1=(octaveNum-1)*binPerOctave*(fftLength/2+1);
	}
	__mcdot1(mRealArr1, mImageArr1, 
			mRealFilterBankArr+index1, mImageFilterBankArr+index1,
		 	timeLength, fftLength/2+1,
		 	binPerOctave, fftLength/2+1, 
		 	mRealArr2, mImageArr2);

	for(int i=0;i<timeLength;i++){
		for(int j=(octaveNum-1)*binPerOctave,k=0;j<octaveNum*binPerOctave;j++,k++){
			float _value1=0;
			float _value2=0;

			_value1=mRealArr2[i*binPerOctave+k];
			_value2=mImageArr2[i*binPerOctave+k];

			// norm => similar fft 'orthi' sqrt(len)
			if(cqtObj->isScale){
				_value1/=sLenArr[j];
				_value2/=sLenArr[j];
			}

			mRealArr3[i*octaveNum*binPerOctave+j]=_value1;
			mImageArr3[i*octaveNum*binPerOctave+j]=_value2;
		}
	}

	// 2. down
	memcpy(preDataArr, dataArr, sizeof(float )*dataLength);
	for(int i=octaveNum-2;i>=0;i--){
		// resample
		curDataLength=resampleObj_resample(resampleObj, preDataArr, preDataLength, curDataArr);
		slideLength/=2;

		// stft t*fftLength
		stftObj_setSlideLength(stftObj, slideLength);
		stftObj_stft(stftObj,curDataArr,curDataLength,mRealArr1,mImageArr1);

		// t*fftLength => t*(fftLength/2+1)
		for(int j=1;j<timeLength;j++){
			for(int k=0;k<(fftLength/2+1);k++){
				mRealArr1[j*(fftLength/2+1)+k]=mRealArr1[j*fftLength+k];
				mImageArr1[j*(fftLength/2+1)+k]=mImageArr1[j*fftLength+k];
			}
		}

		// S.dot(filterBank) t*(fftLength/2+1) @ num*(fftLength/2+1)
		if(vFlag){ // vqt num
			index1=i*binPerOctave*(fftLength/2+1);
		}
		__mcdot1(mRealArr1, mImageArr1, 
				mRealFilterBankArr+index1, mImageFilterBankArr+index1,
			 	timeLength, fftLength/2+1,
			 	binPerOctave, fftLength/2+1, 
			 	mRealArr2, mImageArr2);

		for(int n=0;n<timeLength;n++){
			for(int j=i*binPerOctave,k=0;j<(i+1)*binPerOctave;j++,k++){
				float _value1=0;
				float _value2=0;

				_value1=mRealArr2[n*binPerOctave+k];
				_value2=mImageArr2[n*binPerOctave+k];

				// norm => downsample 默认非scale sqrt(2^i)
				_value1*=dLenArr[octaveNum-i-1];
				_value2*=dLenArr[octaveNum-i-1];

				// norm => similar fft 'orthi' sqrt(len)
				if(cqtObj->isScale){
					_value1/=sLenArr[j];
					_value2/=sLenArr[j];
				}

				mRealArr3[n*octaveNum*binPerOctave+j]=_value1;
				mImageArr3[n*octaveNum*binPerOctave+j]=_value2;
			}
		}

		// deal data
		memset(preDataArr, 0, sizeof(float )*preDataLength);
		memcpy(preDataArr, curDataArr, sizeof(float )*curDataLength);
		memset(curDataArr, 0, sizeof(float )*curDataLength);
		preDataLength=curDataLength;
	}

	free(preDataArr);
	free(curDataArr);

	cqtObj->timeLength=timeLength;
	cqtObj->stftTimeLength=stftTimeLength;

	cqtObj->mRealArr1=mRealArr1;
	cqtObj->mImageArr1=mImageArr1;

	cqtObj->mRealArr2=mRealArr2;
	cqtObj->mImageArr2=mImageArr2;
}

void cqtObj_free(CQTObj cqtObj){
	STFTObj stftObj=NULL; // octaveNum
	ResampleObj resampleObj=NULL;

	float *mRealFilterBankArr=NULL; // num*(fftLength/2+1)
	float *mImageFilterBankArr=NULL;

	float *freBandArr=NULL; // num
	float *lenArr=NULL; // binPerOctave

	float *sLenArr=NULL;
	float *dLenArr=NULL;

	float *mRealArr1=NULL; // stft r,i(timeLength*fftLength) -> power r(timeLength*(fftLength/2+1)) 
	float *mImageArr1=NULL;

	float *mRealArr2=NULL; 
	float *mImageArr2=NULL;

	float *tailDataArr=NULL;
	float *validDataArr=NULL;

	float *mChromaFilterBank=NULL;
	float *mSArr=NULL;

	FFTObj fftObj=NULL; // dct加速
	DCTObj dctObj=NULL;

	FFTObj devFFTObj=NULL;

	float *devDataArr=NULL; // spectral mag&fft mag

	float *devRealArr1=NULL; // fft
	float *devImageArr1=NULL;

	float *devRealArr2=NULL; // ifft
	float *devImageArr2=NULL;

	if(!cqtObj){
		return;
	}

	stftObj=cqtObj->stftObj;
	resampleObj=cqtObj->resampleObj;

	mRealFilterBankArr=cqtObj->mRealFilterBankArr;
	mImageFilterBankArr=cqtObj->mImageFilterBankArr;

	freBandArr=cqtObj->freBandArr;
	lenArr=cqtObj->lenArr;

	sLenArr=cqtObj->sLenArr;
	dLenArr=cqtObj->dLenArr;

	mRealArr1=cqtObj->mRealArr1;
	mImageArr1=cqtObj->mImageArr1;

	mRealArr2=cqtObj->mRealArr2;
	mImageArr2=cqtObj->mImageArr2;

	tailDataArr=cqtObj->tailDataArr;
	validDataArr=cqtObj->validDataArr;

	mChromaFilterBank=cqtObj->mChromaFilterBank;
	mSArr=cqtObj->mSArr;

	fftObj=cqtObj->fftObj;
	dctObj=cqtObj->dctObj;

	devFFTObj=cqtObj->devFFTObj;
	devDataArr=cqtObj->devDataArr;

	devRealArr1=cqtObj->devRealArr1;
	devImageArr1=cqtObj->devImageArr1;

	devRealArr2=cqtObj->devRealArr2;
	devImageArr2=cqtObj->devImageArr2;

	stftObj_free(stftObj);
	resampleObj_free(resampleObj);

	free(mRealFilterBankArr);
	free(mImageFilterBankArr);

	free(freBandArr);
	free(lenArr);

	free(sLenArr);
	free(dLenArr);

	free(mRealArr1);
	free(mImageArr1);

	free(mRealArr2);
	free(mImageArr2);

	free(tailDataArr);
	free(validDataArr);

	free(mChromaFilterBank);
	free(mSArr);

	fftObj_free(fftObj);
	dctObj_free(dctObj);

	fftObj_free(devFFTObj);
	free(devDataArr);

	free(devRealArr1);
	free(devImageArr1);

	free(devRealArr2);
	free(devImageArr2);

	free(cqtObj);
}

// filterBank相关数据
static void _cqtObj_dealFilterBank(CQTObj cqtObj,int num,float minFre,int samplate,
								int binPerOctave,SpectralFilterBankNormalType normType,WindowType winType,
								float factor,float beta,float thresh,int vFlag){
	int fftLength=0; 
	
	float *freBandArr=NULL;
	float *lenArr=NULL;

	float *sLenArr=NULL;
	float *dLenArr=NULL;

	float *mRealFilterBankArr=NULL; // num*(fftLength/2+1)
	float *mImageFilterBankArr=NULL;

	int octaveNum=0;
	int index=0;

	octaveNum=num/binPerOctave;
	index=(octaveNum-1)*binPerOctave;

	lenArr=__vnew(binPerOctave, NULL);
	sLenArr=__vnew(num, NULL);
	dLenArr=__vnew(octaveNum, NULL);

	freBandArr=cqt_calFreArr(minFre,num,binPerOctave);
	fftLength=cqt_calFFTLength(freBandArr[index],samplate,binPerOctave,&factor,&beta);

	// vFlag 1 => vqt 设num 
	mRealFilterBankArr=__vnew((vFlag?num:binPerOctave)*(fftLength/2+1), NULL);
	mImageFilterBankArr=__vnew((vFlag?num:binPerOctave)*(fftLength/2+1), NULL);
	
	cqt_calLengthArr(binPerOctave,freBandArr+index,samplate,
					binPerOctave,
					&factor,&beta,
					lenArr);

	cqt_calLengthArr(num,freBandArr,samplate,
					binPerOctave,
					&factor,&beta,
					sLenArr);

	for(int i=0;i<num;i++){
		sLenArr[i]=sqrtf(sLenArr[i]);
	}

	dLenArr[0]=1;
	for(int i=1;i<octaveNum;i++){
		dLenArr[i]=sqrtf(1<<i);
	}

	// ??? cqt_filterBank替换
	// cqt_downFilterBank(num,freBandArr,samplate,
	// 				binPerOctave,normType,&winType,
	// 				&factor,&beta,&thresh,
	// 				lenArr,fftLength,
	// 				mRealFilterBankArr,mImageFilterBankArr);

	// vFlag 1 => vqt 设num 不能共用top octave freKernal
	index=(vFlag?0:index);
	cqt_downFilterBank(vFlag?num:binPerOctave,freBandArr+index,samplate,
					binPerOctave,normType,&winType,
					&factor,&beta,&thresh,
					lenArr,fftLength,
					mRealFilterBankArr,mImageFilterBankArr);

	cqtObj->fftLength=fftLength;

	cqtObj->num=num;
	cqtObj->octaveNum=octaveNum;
	cqtObj->binPerOctave=binPerOctave;

	cqtObj->mRealFilterBankArr=mRealFilterBankArr;
	cqtObj->mImageFilterBankArr=mImageFilterBankArr;

	cqtObj->freBandArr=freBandArr;
	cqtObj->lenArr=lenArr;

	cqtObj->sLenArr=sLenArr;
	cqtObj->dLenArr=dLenArr;

	cqtObj->samplate=samplate;

	cqtObj->windowType=winType;
	cqtObj->normType=normType;
}

static void _cqtObj_dealResample(CQTObj cqtObj){
	ResampleObj resampleObj=NULL;

	ResampleQualityType type=ResampleQuality_Fast;
	int isScale=1;

	resampleObj_new(&resampleObj,&type,&isScale,NULL);
	resampleObj_setSamplate(resampleObj,2,1); // 降采样

	cqtObj->resampleObj=resampleObj;
}

// stft数据相关 winType rect
static void _cqtObj_dealStftArr(CQTObj cqtObj,int fftLength,int slideLength){
	STFTObj *stftObjArr=NULL;

	int octaveNum=0;
	int radix2Exp=0;

	octaveNum=cqtObj->octaveNum;
	radix2Exp=util_powerTwoBit(fftLength);

	cqtObj->radix2Exp=radix2Exp;
	cqtObj->slideLength=slideLength;
	
	stftObjArr=(STFTObj *)calloc(octaveNum, sizeof(STFTObj ));
	stftObj_new(stftObjArr,radix2Exp,NULL,&slideLength,NULL);

	for(int i=1;i<octaveNum;i++){
		slideLength/=2;
		stftObj_new(stftObjArr+i,radix2Exp,NULL,&slideLength,NULL);
	}	

	// cqtObj->stftObjArr=stftObjArr;
}

static void _cqtObj_dealStft(CQTObj cqtObj,int fftLength,int slideLength,int isContinue){
	STFTObj stftObj=NULL;

	PaddingPositionType pType=PaddingPosition_Right;
	int radix2Exp=0;

	radix2Exp=util_powerTwoBit(fftLength);

	cqtObj->radix2Exp=radix2Exp;
	cqtObj->slideLength=slideLength;
	
	stftObj_new(&stftObj,radix2Exp,NULL,&slideLength,NULL);
	stftObj_enablePadding(stftObj,1); // 默认 center 0 padding

	if(isContinue){ // right 0 padding
		stftObj_setPadding(stftObj, &pType, NULL, NULL, NULL);
	}

	cqtObj->stftObj=stftObj;
}

static int _calRadix2(int length){
	int r=0;
	int m=0;

	while(1){
		m=length%2;
		if(!m){ //
			r++;
			length=length/2;
			if(length==1){
				break;
			}
		}
		else{
			r=0;
			break;
		}
	}

	return r;
}




```

---

### Archivo: `./src/util/flux_util.h`

```


#ifndef FLUX_UTIL_H
#define FLUX_UTIL_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

// 2^n
int util_isPowerTwo(int value);
int util_ceilPowerTwo(int value);
int util_floorPowerTwo(int value);
int util_roundPowerTwo(int value);

// value=2^n =>n
int util_powerTwoBit(int value);

// a>b greatest common divisor
int util_gcd(int a,int b);

// fre
float util_midiToFre(int midi);
int util_freToMidi(float fre);
int util_midiTimes(int midi1,int midi2);
int util_freTimes(float fre1,float fre2);

int util_freToSimularMidi(float fre);
int util_freTimes1(float fre1,float fre2);

// tone
void util_calTone(float value,float *value1,float *value2);
int util_calToneTimes(float value1,float value2,int *type);
int util_calFreTimes(float value1,float value2,int *type);

int util_calRangeTimes(float value1,float value2,int *type);
int util_calApproTimes(float value1,float value2,int *type);

// scale
void util_minMaxScale(float *vArr1,int length,float *vArr2);
void util_standScale(float *vArr1,int length,int type,float *vArr2);
void util_maxAbsScale(float *vArr1,int length,float *vArr2);
void util_robustScale(float *vArr1,int length,float *vArr2);

void util_centerScale(float *vArr1,int length,float *vArr2);
void util_meanScale(float *vArr1,int length,float *vArr2);
void util_arctanScale(float *vArr1,int length,float *vArr2);

// vector norm type type 0 p 1/2/3... 1 Inf 2 -Inf
void util_normalize(float *vArr1,int length,int type,float p,float *vArr2);

// mag/power/DB min=-80 
void util_powerToDB(float *pArr,int length,float min,float *dArr);

void util_powerToAbsDB(float *pArr,int length,int fftLength,int isNorm,float min,float *dArr);
void util_magToAbsDB(float *pArr,int length,int fftLength,int isNorm,float min,float *dArr);

// log compression gamma=1.0 1/10/20/...
void util_logCompress(float *vArr1,float *gamma,int length,float *vArr2);
void util_log10Compress(float *vArr1,float *gamma,int length,float *vArr2);

// temproal, return maxDb, percent is < -base
float util_temproal(float *dataArr,int length,float base,float *avgDb,float *percent);

// gamma eps=1e-5
float util_gamma(float x,float *eps);
long double util_gammal(long double x,long double *eps);

// quadratically interpolated return p ∈[-1/2,1/2]
float util_qaudInterp(float value1,float value2,float value3,float *outValue);

// peak pick
void util_peakPick(float *pArr,int length,int start,int end,int distance,int num,float *vArr,int *cArr);

// order must odd; delta/deltaDelta
void util_delta(float *dataArr1,int length,int order,float *dataArr2);

// pre_emphasis; coef 0.97
void util_preEmphasis(float *vArr1,int length,float coef,float *vArr2);

// synthesized f0; length1=floor(time*fs), ampArr can NULL, default is 1
float *util_synthF0(float *timeArr,float *freArr,int length,int samplate,float *ampArr);

// wave
int util_readWave(char *name,float **dataArr);
void util_writeWave(char *name,float *dataArr,int length);


#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/util/flux_util.c`

```
// 

#include <string.h>
#include <math.h>

#include "../vector/flux_vector.h"
#include "../vector/flux_vectorOp.h"

#include "../dsp/filterDesign_fir.h"

#include "../util/flux_wave.h"
#include "../util/flux_util.h"

static int __isEqual(float value1,float value2);
static int __isGreater(float value1,float value2);
static int __isLess(float value1,float value2);

// 2^n相关
int util_isPowerTwo(int value){
	int flag=1;

	if(value<1){
		flag=0;
	}

	if(value&(value-1)){
		flag=0;
	}

	return flag;
}

int util_ceilPowerTwo(int value){
	int n=1;

	if(value<1){
		return n;
	}

	if(util_isPowerTwo(value)){
		n=value;
	}
	else{
		while(value){
			value>>=1;
			n<<=1;
		}
	}

	return n;
}

int util_floorPowerTwo(int value){
	int n=1;

	if(value<1){
		return n;
	}

	if(util_isPowerTwo(value)){
		n=value;
	}
	else{
		value>>=1;
		while(value){
			value>>=1;
			n<<=1;
		}
	}

	return n;
}

int util_roundPowerTwo(int value){
	int n=1;

	int v1=1;
	int v2=1;

	if(value<1){
		return n;
	}
	
	if(util_isPowerTwo(value)){
		n=value;
	}
	else{
		v1=util_floorPowerTwo(value);
		v2=util_ceilPowerTwo(value);

		if(value-v1<v2-value){
			n=v1;
		}
		else{
			n=v2;
		}
	}

	return n;
}

// value=2^n =>n
int util_powerTwoBit(int value){
	int r=0;
	int m=0;

	if(util_isPowerTwo(value)){
		while(1){
			m=value%2;
			if(!m){ //
				r++;
				value=value/2;
				if(value==1){
					break;
				}
			}
			else{
				r=0;
				break;
			}
		}
	}

	return r;
}

// 最大公约数 a>b 辗转相除
int util_gcd(int a,int b){
	int c=0;

	c=a%b;
	if(c==0){
		return b;
	}
	else{
		return util_gcd(b,c);
	}
}

// tone
float util_freToMidiRange(float fre,int *midi1,int *midi2){
	float per=0;

	float curFre=0;
	float preFre=0;
	float nextFre=0;

	float sub1=0;
	float sub2=0;

	int m1=0;
	int m2=0;

	m1=round(12*log2(fre/440)+69);

	curFre=powf(2,1.0*(m1-69)/12)*440;
	preFre=powf(2,1.0*(m1-1-69)/12)*440;
	nextFre=powf(2,1.0*(m1+1-69)/12)*440;

	sub1=curFre-preFre;
	sub2=nextFre-curFre;

	if(nextFre-fre<fre-preFre){
		m2=m1+1;
	}
	else{
		m2=m1-1;
	}

	if(fre>curFre){
		if(m2==m1+1){
			per=(nextFre-fre)/sub2;
		}
		else{
			per=(sub1-(fre-curFre))/sub1;
		}
	}
	else{
		per=(sub1-(curFre-fre))/sub1;
	}

	if(midi1){
		*midi1=m1;
	}

	if(midi2){
		*midi2=m2;
	}

	return per;
}

void util_calTone(float value,float *value1,float *value2){
	float curFre=0;
	float preFre=0;
	float nextFre=0;

	int midi=0;

	midi=round(12*log2(value/440)+69);

	curFre=powf(2,1.0*(midi-69)/12)*440;
	if(value1){
		*value1=curFre;
	}

	if(value2){
		preFre=powf(2,1.0*(midi-1-69)/12)*440;
		nextFre=powf(2,1.0*(midi+1-69)/12)*440;

		if(nextFre-value<value-preFre){
			*value2=nextFre;
		}
		else{
			*value2=preFre;
		}
	}
}

int util_calToneTimes(float value1,float value2,int *type){
	int k=0;

	float _value=0;

	if(!value1||!value2){
		return 0;
	}

	if(type){
		*type=0;
	}

	if(__isEqual(value1, value2)){ // value1==value2
		k=1;
	}
	else if(__isLess(value1, value2)){ // value1<value2
		k=roundf(value2/value1);
		util_calTone(k*value1, &_value, NULL);
		if(!__isEqual(value2, _value)){
			k=0;
		}
	}
	else { // value1>value2
		k=roundf(value1/value2);
		util_calTone(k*value2, &_value, NULL);
		if(!__isEqual(value1, _value)){
			k=0;
		}

		if(type){
			*type=1;
		}
	}

	return k;
}

int util_calFreTimes(float value1,float value2,int *type){
	int flag=0;

	float _value1=0;
	float _value2=0;

	util_calTone(value1,&_value1,NULL);
	util_calTone(value2,&_value2,NULL);

	flag=util_calToneTimes(_value1,_value2,type);

	return flag;
}

/***
	1. sub:value
	2. sub1:sub2
****/
int util_calRangeTimes(float value1,float value2,int *type){
	int k=0;

	float _value1=0;
	float _value2=0;

	float _select1=0;
	float _select2=0;

	int flag1=0;
	int flag2=0;

	float s1=0;
	float s2=0;

	util_calTone(value1, &_value1, &_select1);
	util_calTone(value2, &_value2, &_select2);
	
	if(value1>660){
		s1=10;
	}
	else if(value1>330){
		s1=5;
	}

	if(fabsf(fabsf(_value1-value1)-fabsf(_select1-value1))<s1){
		flag1=1;
	}

	if(value2>660){
		s2=10;
	}
	else if(value2>330){
		s2=5;
	}

	if(fabsf(fabsf(_value2-value2)-fabsf(_select2-value2))<s2){
		flag2=1;
	}

	k=util_calToneTimes(_value1, _value2, type);
	if(!k&&(value1<330||flag1)){ // 338/340 330->440
		k=util_calToneTimes(_select1, _value2, type);
		if(!k&&(value2<330||flag2)){ // 338/340 330->440
			k=util_calToneTimes(_value1, _select2, type);
			if(!k){
				k=util_calToneTimes(_select1, _select2, type);
			}
		}
	}

	if(k>10){
		float e1=0,e2=0,e3=0;

		e1=fabsf((k-1)*value1-value2);
		e2=fabsf(k*value1-value2);
		e3=fabsf((k+1)*value1-value2);

		if(e1<e2&&e1<e3){
			k--;
		}
		else if(e3<e1&&e3<e2){
			k++;
		}
	}

	return k;
}

int util_calApproTimes(float value1,float value2,int *type){
	int k=0;

	return k;
}

// midi 12*log2(fre/440)+69
float util_midiToFre(int midi){
	float fre=0;

	fre=powf(2,1.0*(midi-69)/12)*440;

	return fre;
}

int util_freToMidi(float fre){
	int midi=0;

	midi=roundf(12*log2(fre/440)+69);

	return midi;
}

int util_midiTimes(int midi1,int midi2){
	int k=0;

	float fre1=0;
	float fre2=0;
	float fre3=0;

	int _m1=0;
	int _m2=0;

	if(midi1>=midi2){
		fre1=util_midiToFre(midi1);
		fre2=util_midiToFre(midi2);
		_m1=midi1;
	}
	else{
		fre1=util_midiToFre(midi2);
		fre2=util_midiToFre(midi1);
		_m1=midi2;
	}

	k=roundf(fre1/fre2);
	fre3=fre2*k;
	_m2=util_freToMidi(fre3);

	if(_m1!=_m2){
		k=0;
	}

	return k;
}

int util_freToSimularMidi(float fre){
	int midi1=0;
	int midi2=0;

	float tone1=0;
	float tone2=0;

	float det=0;
	float _m=0;

	midi1=util_freToMidi(fre);
	tone1=util_midiToFre(midi1);
	if(fre<tone1){
		midi2=midi1-1;
	}
	else{
		midi2=midi1+1;
	}

	tone2=util_midiToFre(midi2);
	det=tone1-tone2;
	_m=tone2+det/2;
	if(fabsf(fre-_m)>fabsf(det)/4){
		midi2=0;
	}

	return midi2;
}

int util_freTimes(float fre1,float fre2){
	int k=0;

	int midi1=0;
	int midi2=0;

	int _midi1=0;
	int _midi2=0;

	midi1=util_freToMidi(fre1);
	midi2=util_freToMidi(fre2);

	_midi1=util_freToSimularMidi(fre1);
	_midi2=util_freToSimularMidi(fre2);

	k=util_midiTimes(midi1,midi2);
	if(!k){
		if(midi1<midi2){
			if(_midi1){ // midi1<64
				k=util_midiTimes(_midi1,midi2);
			}

			if(!k&&_midi2){
				k=util_midiTimes(midi1,_midi2);
			}

			if(!k&&_midi1&&_midi2){
				k=util_midiTimes(_midi1,_midi2);
			}
		}
		else{
			if(_midi2){ // midi2<64
				k=util_midiTimes(midi1,_midi2);
			}

			if(!k&&_midi1){
				k=util_midiTimes(_midi1,midi2);
			}

			if(!k&&_midi1&&_midi2){
				k=util_midiTimes(_midi1,_midi2);
			}
		}
	}

	return k;
}

// scale
void util_minMaxScale(float *vArr1,int length,float *vArr2){

	__vminmaxscale(vArr1,length,vArr2);
}

void util_standScale(float *vArr1,int length,int type,float *vArr2){

	__vstandscale(vArr1,length,type,vArr2);
}

void util_maxAbsScale(float *vArr1,int length,float *vArr2){

	__vmaxabsscale(vArr1,length,vArr2);
}

void util_robustScale(float *vArr1,int length,float *vArr2){

	__vrobustscale(vArr1,length,vArr2);
}

void util_centerScale(float *vArr1,int length,float *vArr2){

	__vcenterscale(vArr1,length,vArr2);
}

void util_meanScale(float *vArr1,int length,float *vArr2){

	__vmeanscale(vArr1,length,vArr2);
}

void util_arctanScale(float *vArr1,int length,float *vArr2){

	__varctanscale(vArr1,length,vArr2);
}

// 向量归一化 type 0 p 1/2/3... 1 Inf 2 -Inf
void util_normalize(float *vArr1,int length,int type,float p,float *vArr2){

	__vnormalize(vArr1,length,type,p,vArr2);
}

float util_rectScale(float cur,float left,float right){
	float d1=0;
	float d2=0;

	d1=right-left;
	d2=(d1>=0)?(right)/(cur+right):(-left)/(cur+left);

	return d2;
}

float util_hannScale(float cur,float left,float right){
	float d1=0;
	float d2=0;

	d1=right-left;
	d2=(d1>=0)?(2*right-cur)/(cur+right):(cur-2*left)/(cur+left);

	return d2;
}

float util_hammScale(float cur,float left,float right){
	float d1=0;
	float d2=0;

	d1=right-left;
	d2=(d1>=0)?(2*right-cur)/(cur+right):(cur-2*left)/(cur+left);

	return d2;
}

void util_powerToDB(float *pArr,int length,float min,float *dArr){
	float max=0;
	float *arr=NULL;

	if(dArr){
		arr=dArr;
	}
	else{
		arr=pArr;
	}

	if(min>=0){
		min=-80;
	}

	__vmax(pArr, length, &max);
	for(int i=0;i<length;i++){
		float _value=0;

		_value=10*log10f(pArr[i]/max);
		arr[i]=(_value>min?_value:min);
	}
}

void util_powerToAbsDB(float *pArr,int length,int fftLength,int isNorm,float min,float *dArr){
	float max=0;
	int maxIndex=0;

	float *arr=NULL;
	float fLen=0;

	if(dArr){
		arr=dArr;
	}
	else{
		arr=pArr;
	}

	if(min>=0){
		min=-80;
	}

	fLen=fftLength*fftLength;
	for(int i=0;i<length;i++){
		float _value=0;

		_value=10*log10f(pArr[i]/fLen);
		arr[i]=(_value>min?_value:min);
	}

	if(isNorm){
		maxIndex=__vmax(pArr, length, NULL);
		max=arr[maxIndex];
		for(int i=0;i<length;i++){
			arr[i]=max-arr[i];
		}
	}
}

void util_magToAbsDB(float *pArr,int length,int fftLength,int isNorm,float min,float *dArr){
	float max=0;
	int maxIndex=0;

	float *arr=NULL;

	if(dArr){
		arr=dArr;
	}
	else{
		arr=pArr;
	}

	if(min>=0){
		min=-80;
	}

	for(int i=0;i<length;i++){
		float _value=0;

		_value=20*log10f(pArr[i]/fftLength);
		arr[i]=(_value>min?_value:min);
	}

	if(isNorm){
		maxIndex=__vmax(pArr, length, NULL);
		max=arr[maxIndex];
		for(int i=0;i<length;i++){
			arr[i]=max-arr[i];
		}
	}
}

void util_logCompress(float *vArr1,float *gamma,int length,float *vArr2){

	__vlog_compress(vArr1, gamma,NULL, length, vArr2);
}

void util_log10Compress(float *vArr1,float *gamma,int length,float *vArr2){

	__vlog10_compress(vArr1, gamma,NULL, length, vArr2);
}

// temproal, return maxDb, percent is < -base
float util_temproal(float *dataArr,int length,float base,float *avgValue,float *percentValue){
	float max=-100;

	int count=0;
	float value=0;
	float total=0;
	
	if(!dataArr||!length){
		return 0;
	}

	for(int i=0;i<length;i++){
		value=20*log10f(fabsf(dataArr[i])+1e-8);
		if(value<-36){
			value=-36;
		}

		if(max<value){
			max=value;
		}

		total+=value;

		if(value>-base){
			count++;
		}
	}

	*avgValue=total/length;
	*percentValue=1.0*(length-count)/length;

	return max;
}

/***
	x=1 1
	0<x<1 
	x>1 递归
	x<0 递归
****/
float util_gamma(float x,float *eps){
	float y=0;
	float err=0;

	int i=1;
	float cur=1.0;
	float pre=0;

	err=1e-5;
	if(eps){
		if(*eps>0){
			err=*eps;
		}
	}

	if(fabs(x-1.0)<err){
		return 1.0;
	}
	else if(fabs(x-0.5)<err){
		return sqrt(M_PI);
	}

	if(x>1.0){
		return (x-1)*util_gamma(x-1, eps);
	}
	else if(x<0){
		return util_gamma(x+1, eps)/x;
	}

	while(fabsf(cur-pre)/cur>err){
		pre=cur;
		cur*=i/(x-1+i);
		i++;
	}
	y=cur*powf(i, x-1);

	return y;
}

long double util_gammal(long double x,long double *eps){
	long double y=0;
	long double err=0;

	int i=1;
	long double cur=1.0;
	long double pre=0;

	err=1e-5;
	if(eps){
		if(*eps>0){
			err=*eps;
		}
	}

	if(fabsl(x-1.0)<err){
		return 1.0;
	}
	else if(fabsl(x-0.5)<err){
		return sqrt(M_PI);
	}

	if(x>1.0){
		return (x-1)*util_gammal(x-1, eps);
	}
	else if(x<0){
		return util_gammal(x+1, eps)/x;
	}

	while(fabsl(cur-pre)/cur>err){
		pre=cur;
		cur*=i/(x-1+i);
		i++;
	}
	y=cur*powl(i, x-1);

	return y;
}

// quadratically interpolated return p ∈[-1/2,1/2]
float util_qaudInterp(float value1,float value2,float value3,float *outValue){
	float p=0;

	p=(value3-value1)/(2*(2*value2-value3-value1)+1e-16);
	if(outValue){
		*outValue=value2-0.25*(value1-value3)*p;
	}

	return p;
}

// peak pick
void util_peakPick(float *pArr,int length,int start,int end,int distance,int num,float *vArr,int *cArr){
	int index1=0;
	int index2=0;

	if(distance<=0){
		distance=1;
	}

	for(int i=0;i<num;i++){
		cArr[i]=__vmax(pArr+start, end-start+1, vArr+i)+start;

		index1=(cArr[i]-distance>start?cArr[i]-distance:start);
		index2=(cArr[i]+distance<end?cArr[i]+distance:end);
		for(int j=index1;j<=index2;j++){
			pArr[j]=NAN;
		}
	}
}

// order must odd; delta/deltaDelta
void util_delta(float *dataArr1,int length,int order,float *dataArr2){
	float *bArr=NULL;
	float aArr[]={1};

	if(order&1){
		bArr=filterDesign_smooth1(order);
		filterDesign_filter(bArr,aArr,dataArr1,
							order,1,length,
							dataArr2);
	}

	free(bArr);
}

// pre emphasis coef 0.97
void util_preEmphasis(float *vArr1,int length,float coef,float *vArr2){

	if(vArr2){
		vArr2[0]=vArr1[0];
		for(int i=1;i<length;i++){
			vArr2[i]=vArr1[i]-coef*vArr1[i-1];
		}
	}
}

// synthesized f0; length1=floor(time*fs), ampArr can NULL, default is 1
float *util_synthF0(float *timeArr,float *freArr,int length,int samplate,float *ampArr){
	float *fArr=NULL;
	float *tArr=NULL;

	float *fArr1=NULL;
	float *tArr1=NULL;
	float *aArr1=NULL;

	float *dataArr=NULL;

	int length1=0;

	float cum=0;

	length1=floorf(timeArr[length-1]*samplate);

	fArr=__vnew(length, NULL);
	tArr=__vnew(length, NULL);

	__vmul_value(timeArr, samplate, length, tArr);
	__vmul_value(freArr, 2*M_PI/samplate, length, fArr);

	fArr1=__vnew(length1, NULL);
	__varange(0, length1, 1, &tArr1);

	__vinterp_linear(tArr,fArr,length,tArr1,length1,fArr1);

	aArr1=__vnew(length1, NULL);
	if(ampArr){
		__vinterp_linear(tArr,ampArr,length,tArr1,length1,aArr1);
	}
	else{
		for(int i=0;i<length1;i++){
			aArr1[i]=1;
		}
	}

	// synth wave
	dataArr=__vnew(length1, NULL);
	for(int i=0;i<length1;i++){
		cum+=fArr1[i];
		dataArr[i]=cum;
	}

	__vsin(dataArr, length1, NULL);
	__vmul(dataArr, aArr1, length1, NULL);

	free(fArr);
	free(tArr);

	free(fArr1);
	free(tArr1);
	free(aArr1);

	return dataArr;
}

int util_readWave(char *name,float **dataArr){
	int status=0;
	WaveReadObj waveRead=NULL;

	int samplate=0;
	int bit=0;
	int channelNum=0;

	int length=0;
	float *_dataArr=NULL;
	
	status=waveReadObj_new(&waveRead,name);
	if(!status){
		length=waveReadObj_getInfor(waveRead,&samplate,&bit,&channelNum);
		_dataArr=__vnew(length, NULL);

		waveReadObj_read(waveRead, _dataArr, length);
		*dataArr=_dataArr;

		waveReadObj_free(waveRead);
	}

	return length;
}

void util_writeWave(char *name,float *dataArr,int length){
	int status=0;

	WaveWriteObj waveWrite=NULL;

	int samplate=32000;
	int bit=16;
	int channelNum=1;

	status=waveWriteObj_new(&waveWrite,name,
							&samplate,&bit,&channelNum);
	if(!status){
		waveWriteObj_write(waveWrite,dataArr,length);
		waveWriteObj_free(waveWrite);
	}
}

static int __isEqual(float value1,float value2){
	int flag=0;

	if(fabsf(value1-value2)<0.81){
		return 1;
	}

	return flag;
}

static int __isGreater(float value1,float value2){
	int flag=0;

	if(value1-value2>0.81){
		return 1;
	}

	return flag;
}

static int __isLess(float value1,float value2){
	int flag=0;

	if(value2-value1>0.81){
		return 1;
	}


	return flag;
}










```

---

### Archivo: `./src/util/flux_wave.c`

```
// 

#include <string.h>
#include <math.h>

#include "../vector/flux_vector.h"
#include "../vector/flux_vectorOp.h"

#include "flux_wave.h"

typedef struct  {
	// RIFF chunk 12
	char riff[4]; // "riff"
	unsigned int size;
	char wav[4];  // "WAVE"

	// fmt sub-chunk >=20
	char fmt[4];  // "fmt "
	unsigned int fmtSize; // >=16 

	unsigned short format; // 1/3/... 
	unsigned short channelNum;

	unsigned int samplate;
	unsigned int byteRate;

	unsigned short blockAlign; 
	unsigned short bit;

	// data sub-chunk 8
	char data[4]; // "data"
	unsigned int dataSize;
} WavHeader;

struct OpaqueWaveRead{
	FILE *fp;

	int samplate;
	int bit;
	int channelNum;

	unsigned short format;

	int dataLength; // head data totalLength
	int curLength; // read
};

struct OpaqueWaveWrite{
	FILE *fp;

	int samplate;
	int bit;
	int channelNum;

	unsigned int fmt_size; 

	int curLength; // write
};

char __wav_header[44]={ 
						0x52, 0x49, 0x46, 0x46, 0x00, 0x00, 0x00, 0x00,
						0x57, 0x41, 0x56, 0x45, 0x66, 0x6d, 0x74, 0x20,
						0x10, 0x00, 0x00, 0x00, 0x01, 0x00, 0x00, 0x00,
						0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
						0x00, 0x00, 0x00, 0x00, 0x64, 0x61, 0x74, 0x61,
						0x00, 0x00, 0x00, 0x00 
};

static int __readChunkSize(FILE *file);
static void __readChunkName(FILE *file);

int waveReadObj_new(WaveReadObj *waveObj,char *fileName){
	int status=0;
	WaveReadObj wave=NULL;

	FILE *fp=NULL;
	WavHeader header;

	unsigned int offset=0;
	unsigned int dataSize=0;

	char *chunkName=NULL;

	wave=*waveObj=(WaveReadObj )calloc(1, sizeof(struct OpaqueWaveRead ));
	fp=fopen(fileName, "rb");

	fread(&header, 1, sizeof(header), fp);
	if(header.fmtSize<16){
		printf("wav is error!!!\n");

		fclose(fp);
		free(wave);
		return 1;
	}

	// printf("fmt_size is %d\n",header.fmt_size);
	// printf("format is %d\n",header.format);

	offset=20+header.fmtSize+4; // ???
	fseek(fp, offset, SEEK_SET);

	// LIST
	chunkName=(char *)calloc(5, sizeof(char ));
	strncpy(chunkName,header.data,4);
	while(strncmp(chunkName, "data", 4)){
		int skipSize=0;

		fread(&skipSize, 1, sizeof(int ), fp);
		offset+=4;

		offset+=skipSize;
		fseek(fp, offset, SEEK_SET);
		fread(chunkName, 4, sizeof(char ), fp);

		offset+=4;
	}

	fseek(fp, offset, SEEK_SET);
	fread(&dataSize, 1, sizeof(unsigned int ), fp);

	wave->fp=fp;

	wave->samplate=header.samplate;
	wave->channelNum=header.channelNum;
	wave->bit=header.bit;

	wave->format=header.format;

	wave->dataLength=dataSize/(header.bit/ 8);

	free(chunkName);
	return status;
}

int waveReadObj_getInfor(WaveReadObj waveObj,int *samplate,int *bit,int *channelNum){
	int dataLength=0;

	if(samplate){
		*samplate=waveObj->samplate;
	}

	if(channelNum){
		*channelNum=waveObj->channelNum;
	}

	if(bit){
		*bit=waveObj->bit;
	}

	dataLength=waveObj->dataLength;
	return dataLength;
}

int waveReadObj_read(WaveReadObj waveObj,float *dataArr,int dataLength1){
	FILE *fp=NULL;
	int bit=0;

	int channelNum=0;

	unsigned short format;

	int dataLength=0;
	int curLength=0;

	int subLen=0;

	fp=waveObj->fp;
	bit=waveObj->bit;
	if(bit!=8&&bit!=16&&bit!=32){
		return 0;
	}

	channelNum=waveObj->channelNum;
	if(dataLength1%channelNum!=0){
		return 0;
	}

	format=waveObj->format;
	if(format!=1&&format!=3){ // PCM/IEEE float
		return 0;
	}

	dataLength=waveObj->dataLength;
	curLength=waveObj->curLength;

	if(curLength+dataLength1>dataLength){
		subLen=dataLength-(curLength+dataLength1);
	}

	for(int i=curLength,j=0;i<curLength+dataLength1-subLen;i++,j++){
		if(bit==8){
			char v1=0;

			fread(&v1, 1, sizeof(char ), fp);
			dataArr[j]=1.0*v1/(1<<7);
		}
		else if(bit==16){
			short v1=0;

			fread(&v1, 1, sizeof(short ), fp);
			dataArr[j]=1.0*v1/(1<<15);
		}
		else{
			if(format==1){ // 1 --> PCM/uncompressed
				int v1=0;

				// 1<<31 -2147483648
				fread(&v1, 1, sizeof(int ), fp);
				dataArr[j]=-1.0*v1/(1<<31);
			}
			else { // 3 --> IEEE float ???
				fread(dataArr+j, 1, sizeof(float ), fp);
			}
		}
	}

	waveObj->curLength=curLength+dataLength1-subLen;
	return dataLength1-subLen;
}

void waveReadObj_free(WaveReadObj waveObj){

	if(waveObj){
		fclose(waveObj->fp);
		free(waveObj);
	}
}

int waveWriteObj_new(WaveWriteObj *waveObj,char *fileName,
					int *samplate,int *bit,int *channelNum){
	int status=0;
	WaveWriteObj wave=NULL;

	FILE *fp=NULL;
	WavHeader header;

	int _samplate=32000;
	int _bit=16;
	int _channelNum=1;

	wave=*waveObj=(WaveWriteObj )calloc(1, sizeof(struct OpaqueWaveWrite ));
	fp=fopen(fileName, "wb");

	if(samplate){
		if(*samplate>0&&*samplate<=196000){
			_samplate=*samplate;
		}
	}

	if(bit){
		if(*bit==8||*bit==16||*bit==32){
			_bit=*bit;
		}
	}

	if(_channelNum){
		if(*channelNum>0){
			_channelNum=*channelNum;
		}
	}

	memcpy(&header, __wav_header, sizeof(header));
	header.channelNum=_channelNum;
	header.bit=_bit;
	header.samplate=_samplate;
	header.byteRate = _samplate*_channelNum*(_bit/8);
	header.blockAlign= _channelNum*(_bit/8);

	fwrite(&header, 1, sizeof(header), fp);

	wave->fp=fp;

	wave->samplate=_samplate;
	wave->bit=_bit;
	wave->channelNum=_channelNum;

	wave->samplate=header.samplate;
	wave->channelNum=header.channelNum;
	wave->bit=header.bit;

	wave->fmt_size=header.fmtSize;

	return status;
}

int waveWriteObj_write(WaveWriteObj waveObj,float *dataArr,int dataLength){
	FILE *fp=NULL;

	int bit=0;
	int channelNum=0;

	int curLength=0;

	unsigned int offset=0;
	unsigned int _size=0;
	unsigned int _dataSize=0;

	fp=waveObj->fp;

	bit=waveObj->bit;
	channelNum=waveObj->channelNum;
	if(dataLength%channelNum!=0){
		return 0;
	}

	curLength=waveObj->curLength;

	for(int i=0;i<dataLength;i++){
		if(bit==8){
			char v1=0;

			if(dataArr[i]>=1.0){
				v1=(1<<7)-1;
			}
			else if(dataArr[i]<=-1.0){
				v1=-(1<<7);
			}
			else{
				v1=round(dataArr[i]*(1<<7));
			}
			
			fwrite(&v1, 1, sizeof(char ), fp);
		}
		else if(bit==16){
			short v1=0;

			if(dataArr[i]>=1.0){
				v1=(1<<15)-1;
			}
			else if(dataArr[i]<=-1.0){
				v1=-(1<<15);
			}
			else{
				v1=round(dataArr[i]*(1<<15));
			}

			fwrite(&v1, 1, sizeof(short ), fp);
		}
		else{ // 32 fmt 1
			/***
				int 1<<31 -2147483648 !!!
			****/
			int v1=0;

			if(dataArr[i]>=1.0){
				v1=-((1<<31)+1);
			}
			else if(dataArr[i]<=-1.0){
				v1=(1<<31);
			}
			else {
				v1=-round(dataArr[i]*(1<<31));
			}
			
			fwrite(&v1, 1, sizeof(int ), fp);
			
			// fwrite(dataArr+i, 1, sizeof(float ), fp);
		}
	}

	_dataSize=(curLength+dataLength)*(bit/8);
	_size=sizeof(WavHeader )-8+_dataSize;

	offset=4;
	fseek(fp, offset, SEEK_SET);
	fwrite(&_size, 1, sizeof(unsigned int ), fp);

	offset=20+waveObj->fmt_size+4;
	fseek(fp, offset, SEEK_SET);
	fwrite(&_dataSize, 1, sizeof(unsigned int ), fp);

	fseek(fp, 0, SEEK_END);

	waveObj->curLength=curLength+dataLength; // update
	return dataLength;
}

void waveWriteObj_free(WaveWriteObj waveObj){

	if(waveObj){
		fclose(waveObj->fp);
		free(waveObj);
	}
}











```

---

### Archivo: `./src/util/flux_wave.h`

```


#ifndef FLUX_WAVE_H
#define FLUX_WAVE_H

#ifdef __cplusplus
extern "C" {
#endif

#include <stdio.h>
#include <stdlib.h>

typedef struct OpaqueWaveRead *WaveReadObj;
typedef struct OpaqueWaveWrite *WaveWriteObj;

int waveReadObj_new(WaveReadObj *waveObj,char *fileName);
int waveReadObj_getInfor(WaveReadObj waveObj,int *samplate,int *bit,int *channelNum);
int waveReadObj_read(WaveReadObj waveObj,float *dataArr,int dataLength);
void waveReadObj_free(WaveReadObj waveObj);

/***
	samplate 32000
	bit 16
	channelNum 1
****/
int waveWriteObj_new(WaveWriteObj *waveObj,char *fileName,
					int *samplate,int *bit,int *channelNum);
int waveWriteObj_write(WaveWriteObj waveObj,float *dataArr,int dataLength);
void waveWriteObj_free(WaveWriteObj waveObj);

#ifdef __cplusplus
}
#endif

#endif
```

---

### Archivo: `./src/stft_algorithm.c`

```
// 

#include <string.h>
#include <math.h>

#include "vector/flux_vector.h"
#include "vector/flux_vectorOp.h"

#include "dsp/flux_window.h"
#include "dsp/fft_algorithm.h"

#include "stft_algorithm.h"

#ifdef HAVE_OMP
#include <omp.h>
#endif

// cpu core number
int __kernelNum=0;

typedef enum{
	STFTExec_None=0,

	STFTExec_STFT,
	STFTExec_ISTFT,

} STFTExecType;

struct OpaqueSTFT{
	STFTExecType execType;
	int useFlag;

	FFTObj fftObj;
	FFTObj *fftObjArr;

	WindowType windowType;
	float *windowDataArr;
	float *addDataArr;

	int fftLength; // y=fftLength ???
	int slideLength;
	int isContinue;

	int isPad; 
	PaddingPositionType positionType; // center
	PaddingModeType modeType; // constant zero

	float padValue1; // center/left/right constant
	float padValue2; // center constant

	float *tailDataArr;
	int tailDataLength;

	float *curDataArr;
	int curDataLength; // >=dataLength

	int timeLength; // x=timeLength

	float *realArr; // fft r cache

	// inverse 
	int methodType; // 0 'overlap-add' 1 'weight overlap-add'

	float *winArr1; // fftLength
	float *winArr2;
	
	int timeLength1;
	float *normArr; // (timeLength1-1)*slideLength+fftLength

	// int _weakFlag; // curDataArr weak flag
};

static void __calTimeAndTailLen(int dataLength,int fftLength,int slideLength,int isPad,int *timeLength,int *tailLength);

// status 0 error
static int __stftObj_dealData(STFTObj stftObj,float *dataArr,int dataLength);

static int __stftObj_dealPadData(STFTObj stftObj,float *dataArr,int dataLength,int tLen,float *curDataArr);

static void __stftObj_stft(STFTObj stftObj,float *dataArr,float *mRealArr,float *mImageArr);

static int __isCOA(float *winArr,int winLength,int overlapLength);

int stftObj_new(STFTObj *stftObj,int radix2Exp,WindowType *windowType,int *slideLength,int *isContinue){
	int status=0;

	int _isContinue=0;
	WindowType _windowType=Window_Rect;
	float *windowDataArr=NULL;
	float *addDataArr=NULL;

	STFTObj stft=NULL;
	FFTObj fftObj=NULL;

	if (__kernelNum==0){
        #ifdef HAVE_OMP
        __kernelNum=omp_get_max_threads()/2;
        if (__kernelNum==0){
            __kernelNum=1;
        }
        #else
        __kernelNum=1;
        #endif
	}

	FFTObj *fftObjArr=(FFTObj *)calloc(__kernelNum, sizeof(FFTObj ));

	int fftLength=0;
	int _slideLength=0;
	float *realArr=NULL;

	float *tailDataArr=NULL;

	if(radix2Exp<1||radix2Exp>30){
		status=-100;
		return status;
	}

	fftLength=1<<radix2Exp;
	if(windowType){
		_windowType=*windowType;
	}

	_slideLength=fftLength/4;
	if(slideLength){
		if(*slideLength>0){ // &&*slideLength<=fftLength ->support not overlap
			_slideLength=*slideLength;
		}
	}

	if(isContinue){
		_isContinue=*isContinue;
	}

	stft=*stftObj=(STFTObj )calloc(1, sizeof(struct OpaqueSTFT ));

	windowDataArr=window_calFFTWindow(_windowType,fftLength);
	addDataArr=__vnew(fftLength, NULL);
	fftObj_new(&fftObj, radix2Exp);

    #pragma omp parallel for
	for(int i=0;i<__kernelNum;i++){
		fftObj_new(fftObjArr+i, radix2Exp);
	}

	realArr=(float *)calloc(fftLength, sizeof(float ));
	tailDataArr=(float *)calloc(fftLength, sizeof(float ));

	stft->tailDataArr=tailDataArr;

	stft->windowType=_windowType;
	stft->windowDataArr=windowDataArr;
	stft->addDataArr=addDataArr;

	stft->fftObj=fftObj;
	stft->fftLength=fftLength;
	stft->slideLength=_slideLength;

	stft->realArr=realArr;
	stft->isContinue=_isContinue;

	stft->isPad=0;
	stft->positionType=PaddingPosition_Center;
	stft->modeType=PaddingMode_Constant;
	stft->fftObjArr=fftObjArr;

	return status;
}

// default 512 fftLength/4
void stftObj_setSlideLength(STFTObj stftObj,int slideLength){
	int fftLength=0;

	fftLength=stftObj->fftLength;
	if(slideLength>0){ // &&slideLength<=fftLength support not overlap
		stftObj->slideLength=slideLength;
	}
}

void stftObj_enableContinue(STFTObj stftObj,int flag){

	stftObj->isContinue=flag;
}

// center zero padding
void stftObj_enablePadding(STFTObj stftObj,int flag){

	stftObj->isPad=flag;
}

// value1 => constant/left
void stftObj_setPadding(STFTObj stftObj,
					PaddingPositionType *positionType,PaddingModeType *modeType,
					float *value1,float *value2){

	if(stftObj->isPad){
		if(positionType){
			stftObj->positionType=*positionType;
		}

		if(modeType){
			stftObj->modeType=*modeType;
		}

		if(value1){
			stftObj->padValue1=*value1;
		}

		if(value2){
			stftObj->padValue2=*value2;
		}
	}
}

void stftObj_useWindowDataArr(STFTObj stftObj,float *winDataArr){
	stftObj->useFlag=1;
	memcpy(stftObj->windowDataArr, winDataArr, sizeof(float )*stftObj->fftLength);
}

float *stftObj_getWindowDataArr(STFTObj stftObj){

	return stftObj->windowDataArr;
}

int stftObj_calTimeLength(STFTObj stftObj,int dataLength){
	int fftLength=0; 
	int slideLength=0;
	int tailDataLength=0;

	int isContinue=0;
	int isPad=0;

	int timeLength=0;

	fftLength=stftObj->fftLength;
	slideLength=stftObj->slideLength;
	tailDataLength=stftObj->tailDataLength;

	isContinue=stftObj->isContinue;
	isPad=stftObj->isPad;

	if(!isPad){
		if(isContinue){
			dataLength+=tailDataLength;
		}

		if(dataLength<fftLength){
			return 0;
		}

		timeLength=(dataLength-fftLength)/slideLength+1;
	}
	else{
		if(dataLength<=0){
			return 0;
		}

		timeLength=dataLength/slideLength+1;
	}

	return timeLength;
}

void stftObj_stft(STFTObj stftObj,float *dataArr,int dataLength,float *mRealArr,float *mImageArr){
	int status=0;

	if(!dataArr||dataLength<=0){
		return;
	}

	// 1. 处理相关数据
	if (stftObj->isPad || stftObj->isContinue) {
	    status=__stftObj_dealData(stftObj,dataArr,dataLength);
        if(!status){
            return;
        }
	}
	else{
	    stftObj->timeLength = stftObj_calTimeLength(stftObj, dataLength);
	}

	// 2. stft
	__stftObj_stft(stftObj,dataArr,mRealArr,mImageArr);
	
	stftObj->execType=STFTExec_STFT;

}

int stftObj_calDataLength(STFTObj stftObj,int timeLength){
	int fftLength=0; // y=fftLength ???
	int slideLength=0;

	int dataLength=0;

	fftLength=stftObj->fftLength;
	slideLength=stftObj->slideLength;

	dataLength=(timeLength-1)*slideLength+fftLength;

	return dataLength;
}

// type 0(deault) 'weight overlap-add' 1 'overlap-add'
void stftObj_istft(STFTObj stftObj,float *mRealArr,float *mImageArr,int timeLength1,int methodType,float *dataArr){
	FFTObj fftObj=NULL;
	float *windowDataArr=NULL;

	int fftLength=0; // y=fftLength ???
	int slideLength=0;

	int dataLength=0;

	float *winArr1=NULL; // fftLength
	float *winArr2=NULL;

	float *normArr=NULL; // (timeLength1-1)*slideLength+fftLength;

	float *realArr=NULL;
	float *imageArr=NULL;

	fftObj=stftObj->fftObj;
	windowDataArr=stftObj->windowDataArr;

	fftLength=stftObj->fftLength;
	slideLength=stftObj->slideLength;

	dataLength=(timeLength1-1)*slideLength+fftLength;

	normArr=stftObj->normArr;

	realArr=__vnew(fftLength, NULL);
	imageArr=__vnew(fftLength, NULL);

	// 1. winArr1/winArr2
	if(!stftObj->winArr1){
		float e=0;

		winArr1=__vnew(fftLength, NULL);
		winArr2=__vnew(fftLength, NULL);
		
		if(methodType==0){ // 'weight'
			e=1;
		}
		else{ // 'overlap-add' 
			e=0;
		}

		__vpow(windowDataArr, e, fftLength, winArr1);
		__vpow(windowDataArr, e+1, fftLength, winArr2);

		stftObj->winArr1=winArr1;
		stftObj->winArr2=winArr2;

		stftObj->methodType=methodType;
	}
	else{
		winArr1=stftObj->winArr1;
		winArr2=stftObj->winArr2;
		if(stftObj->methodType!=methodType){
			float e=0;

			if(methodType==0){ // 'weight'
				e=1;
			}
			else{ // 'overlap-add'
				e=0;
			}

			__vpow(windowDataArr, e, fftLength, winArr1);
			__vpow(windowDataArr, e+1, fftLength, winArr2);

			stftObj->methodType=methodType;
		}
	}

	// 2. normArr
	if(timeLength1>stftObj->timeLength1||
		stftObj->timeLength1>2*timeLength1){

		free(normArr);
		normArr=__vnew(dataLength, NULL);

		stftObj->normArr=normArr;
		stftObj->timeLength1=timeLength1;
	}

	// 3. ifft&overlap add
	memset(normArr, 0, sizeof(float )*dataLength);
	for(int i=0;i<timeLength1;i++){
		fftObj_ifft(fftObj, mRealArr+i*fftLength, mImageArr+i*fftLength, realArr, imageArr);
		
		for(int j=i*slideLength,k=0;j<i*slideLength+fftLength;j++,k++){
			dataArr[j]=dataArr[j]+realArr[k]*winArr1[k];
			normArr[j]=normArr[j]+winArr2[k];
		}
	}

	// 4. norm
	for(int i=0;i<dataLength;i++){
		if(normArr[i]<1e-6){
			normArr[i]=1;
		}
	}

	__vdiv(dataArr, normArr, dataLength, NULL);

	free(realArr);
	free(imageArr);
}

void stftObj_free(STFTObj stftObj){
	FFTObj fftObj=NULL;
	FFTObj *fftObjArr=NULL;

	float *windowDataArr=NULL;
	float *addDataArr=NULL;
	float *tailDataArr=NULL;
	float *curDataArr=NULL;

	float *realArr=NULL;

	float *winArr1=NULL; // fftLength
	float *winArr2=NULL;

	float *normArr=NULL;

	if(!stftObj){
		return;
	}

	fftObj=stftObj->fftObj;
	fftObjArr=stftObj->fftObjArr;

	windowDataArr=stftObj->windowDataArr;
	addDataArr=stftObj->addDataArr;
	tailDataArr=stftObj->tailDataArr;
	curDataArr=stftObj->curDataArr;

	realArr=stftObj->realArr;

	winArr1=stftObj->winArr1;
	winArr2=stftObj->winArr2;

	normArr=stftObj->normArr;

	fftObj_free(fftObj);

    #pragma omp parallel for
	for(int i=0;i<__kernelNum;i++){
		fftObj_free(fftObjArr[i]);
	}
	free(fftObjArr);

	free(windowDataArr);
	free(addDataArr);
	free(tailDataArr);
	free(curDataArr);

	free(realArr);

	free(winArr1);
	free(winArr2);

	free(normArr);

	free(stftObj);
}

/***
	1. 根据isContinue处理curDataArr
	2. 计算stftLength
	3. 处理tailDataArr
****/
static int __stftObj_dealData(STFTObj stftObj,float *dataArr,int dataLength){
	int status=1;

	int fftLength=0; 
	int slideLength=0;

	int isContinue=0;
	int isPad=0;

	float *tailDataArr=NULL;
	int tailDataLength=0;

	float *curDataArr=NULL;
	int curDataLength=0; 

	int timeLength=0;

	int timeLen=0;
	int tailLen=0;

	int totalLength=0;

	fftLength=stftObj->fftLength;
	slideLength=stftObj->slideLength;

	isContinue=stftObj->isContinue;
	isPad=stftObj->isPad;

	tailDataArr=stftObj->tailDataArr;
	tailDataLength=stftObj->tailDataLength;

	curDataArr=stftObj->curDataArr;
	curDataLength=stftObj->curDataLength;

	timeLength=stftObj->timeLength;

	// 1. curDataArr相关
	if(!isPad){ // 非填充
		if(isContinue){
			totalLength=tailDataLength+dataLength;
		}
		else{
			totalLength=dataLength;
		}

		if(totalLength<fftLength){
			tailLen=totalLength;
			status=0;
		}

		if(status){
			__calTimeAndTailLen(totalLength, fftLength, slideLength,isPad, &timeLen, &tailLen);
		}
	}
	else{ // 填充
		totalLength=dataLength;
		__calTimeAndTailLen(totalLength, fftLength, slideLength,isPad, &timeLen, &tailLen);
	}

	if(status){ // 存在timeLen 计算curDataArr相关
		if(totalLength>curDataLength||
			curDataLength>2*totalLength){

			free(curDataArr);
			curDataArr=(float *)calloc(totalLength+fftLength, sizeof(float ));
		}

		curDataLength=0;
		if(!isPad){ // 非填充fftLength
			if(isContinue&&tailDataLength<0){
				memcpy(curDataArr, dataArr-tailDataLength, (dataLength+tailDataLength)*sizeof(float ));
				curDataLength=(dataLength+tailDataLength);
			}
			else{
				if(isContinue&&tailDataLength>0){ // 连续且存在尾数据
					memcpy(curDataArr, tailDataArr, tailDataLength*sizeof(float ));
					curDataLength+=tailDataLength;
				}

				memcpy(curDataArr+curDataLength, dataArr, dataLength*sizeof(float ));
				curDataLength+=dataLength;
			}
		}
		else{ // 填充
			// tailLen=0; // padding is use tailLen
			curDataLength=__stftObj_dealPadData(stftObj,dataArr,dataLength,tailLen,curDataArr);
		}

		// 2. tailDataArr相关
		tailDataLength=0; // reset !!!
		if(isContinue&&!isPad){ // 连续非填充且存在tail
			if(tailLen>0){
				memcpy(tailDataArr,curDataArr+(curDataLength-tailLen),tailLen*sizeof(float ));
			}
			
			tailDataLength=tailLen;
		}
	}
	else{
		// 2. tailDataArr相关
		if(isContinue&&!isPad){ // 连续非填充且存在tail
			if(tailLen>0){
				if(tailDataLength>=0){
					memcpy(tailDataArr+tailDataLength,dataArr,dataLength*sizeof(float ));
				}
				else{
					memcpy(tailDataArr,dataArr-tailDataLength,(dataLength+tailDataLength)*sizeof(float ));
				}
			}
			
			tailDataLength=tailLen;
		}
		else{
			tailDataLength=0;
		}
	}

	// 3. 更新
	stftObj->tailDataLength=tailDataLength;

	stftObj->curDataArr=curDataArr;
	stftObj->curDataLength=curDataLength;

	stftObj->timeLength=timeLen;
	return status;
}

static int __stftObj_dealPadData(STFTObj stftObj,float *dataArr,int dataLength,int tLen,float *curDataArr){
	int fftLength=0; 
	int slideLength=0;

	int isContinue=0;
	int isPad=0;

	float *tailDataArr=NULL;
	int tailDataLength=0;

	int curDataLength=0; 

	float value1=0;
	float value2=0;

	int totalLength=0;
	int startIndex=0;

	int leftLen=0;
	int rightLen=0;

	fftLength=stftObj->fftLength;
	slideLength=stftObj->slideLength;

	isContinue=stftObj->isContinue;
	isPad=stftObj->isPad;

	tailDataArr=stftObj->tailDataArr;
	tailDataLength=stftObj->tailDataLength;

	value1=stftObj->padValue1;
	value2=stftObj->padValue2;

	// 1. 拼接数据
	if(stftObj->positionType==PaddingPosition_Center){
		startIndex=fftLength/2;
	}
	else if(stftObj->positionType==PaddingPosition_Left){
		startIndex=fftLength;
	}
	else if(stftObj->positionType==PaddingPosition_Right){
		startIndex=0;
	}

	// if(isContinue&&tailDataLength){ // 连续且存在尾数据
	// 	memcpy(curDataArr+startIndex, tailDataArr, tailDataLength*sizeof(float ));
	// 	curDataLength+=tailDataLength;
	// }
	
	if(dataLength>tLen){ // ??? 注意临界值问题
		memcpy(curDataArr+(startIndex+curDataLength), dataArr, (dataLength-tLen)*sizeof(float ));
	}
	curDataLength+=(dataLength-tLen);

	// 2. 填充数据
	leftLen=fftLength/2;
	rightLen=fftLength-fftLength/2;
	if(stftObj->modeType==PaddingMode_Constant){
		if(stftObj->positionType==PaddingPosition_Center){ // constant 两边填充
			__vpad_center1(curDataArr,curDataLength,leftLen,rightLen,value1,value2);
		}
		else if(stftObj->positionType==PaddingPosition_Left){ // 头部填充
			__vpad_left1(curDataArr,curDataLength,fftLength,value1);
		}
		else if(stftObj->positionType==PaddingPosition_Right){ // 尾部填充
			__vpad_right1(curDataArr,curDataLength,fftLength,value1);
		}
	}
	else if(stftObj->modeType==PaddingMode_Reflect&&curDataLength>1){ // reflect 反射
		if(stftObj->positionType==PaddingPosition_Center){ // 两边填充
			__vpad_center2(curDataArr,curDataLength,leftLen,rightLen);
		}
		else if(stftObj->positionType==PaddingPosition_Left){ // 开始填充
			__vpad_left2(curDataArr,curDataLength,fftLength);
		}
		else if(stftObj->positionType==PaddingPosition_Right){ // 尾部填充
			__vpad_right2(curDataArr,curDataLength,fftLength);
		}
	}
	else if(stftObj->modeType==PaddingMode_Wrap&&curDataLength>1){ // wrap 
		if(stftObj->positionType==PaddingPosition_Center){ // 两边填充
			__vpad_center3(curDataArr,curDataLength,leftLen,rightLen);
		}
		else if(stftObj->positionType==PaddingPosition_Left){ // 开始填充
			__vpad_left3(curDataArr,curDataLength,fftLength);
		}
		else if(stftObj->positionType==PaddingPosition_Right){ // 尾部填充
			__vpad_right3(curDataArr,curDataLength,fftLength);
		}
	}

	totalLength=curDataLength+fftLength;
	return totalLength;
}

static void __fft(STFTObj stftObj,FFTObj fftObj,int step,float *dataArr,float *mRealArr,float *mImageArr){
	int fftLength=0;
	int slideLength=0;

	float *windowDataArr=NULL;
	float *addDataArr=NULL;

	fftLength=stftObj->fftLength;
	slideLength=stftObj->slideLength;
	windowDataArr=stftObj->windowDataArr;
	addDataArr=__vnew(fftLength, NULL);

	for(int i=0;i<step;i++){
		__vmul(dataArr+i*slideLength, windowDataArr, fftLength, addDataArr);
//		__vdebug(addDataArr, fftLength, 1);
		fftObj_fft(fftObj,addDataArr,NULL,mRealArr+i*fftLength,mImageArr+i*fftLength);
	}

	free(addDataArr);
}

static void __stftObj_stft(STFTObj stftObj,float *dataArr, float *mRealArr,float *mImageArr){
	FFTObj fftObj=NULL;
	FFTObj *fftObjArr=NULL;
	int useFlag=0;

	WindowType windowType=Window_Rect;

	float *curDataArr=NULL;
	float *windowDataArr=NULL;
	float *addDataArr=NULL;

	int fftLength=0;
	int slideLength=0;
	int timeLength=0;// x=curSTFTCount

	int k=0;
	int block=0;
	int mod=0;

//	float *realArr=NULL;
    float *_arr = NULL;

	fftObj=stftObj->fftObj;
	fftObjArr=stftObj->fftObjArr;

	useFlag=stftObj->useFlag;

	windowType=stftObj->windowType;

	curDataArr=stftObj->curDataArr;
	windowDataArr=stftObj->windowDataArr;
	addDataArr=stftObj->addDataArr;

	fftLength=stftObj->fftLength;
	slideLength=stftObj->slideLength;
	timeLength=stftObj->timeLength;

//	realArr=stftObj->realArr;

	k=__kernelNum;
    block=timeLength/k;
    mod=timeLength%k;

    if (stftObj->isPad||stftObj->isContinue){
        _arr=curDataArr;
    }
    else{
        _arr=dataArr;
    }

    #ifdef HAVE_OMP
    if(timeLength==1){
        __fft(stftObj,fftObj,1,_arr,mRealArr,mImageArr);
    }else if(timeLength<__kernelNum){
        omp_set_num_threads(timeLength);

        #pragma omp parallel for
        for(int i=0;i<timeLength;i++){
            __fft(stftObj,fftObjArr[i],1,_arr+i*slideLength,mRealArr+i*fftLength,mImageArr+i*fftLength);
        }
    }else{
        omp_set_num_threads(__kernelNum);

        #pragma omp parallel for
        for(int i=0;i<k;i++){
            __fft(stftObj,fftObjArr[i],block,_arr+i*block*slideLength,mRealArr+i*block*fftLength,mImageArr+i*block*fftLength);
        }

        if(mod){
            __fft(stftObj,fftObj,mod,_arr+k*block*slideLength,mRealArr+k*block*fftLength,mImageArr+k*block*fftLength);
        }
    }
    #else
    for(int i=0;i<timeLength;i++){
        // memcpy(realArr, curDataArr+i*slideLength, sizeof(float )*fftLength);
        // fftObj_fft(fftObj,realArr,NULL,mRealArr+i*fftLength,mImageArr+i*fftLength);

        if(useFlag||windowType!=Window_Rect){
            __vmul(_arr+i*slideLength, windowDataArr, fftLength, addDataArr);
            fftObj_fft(fftObj,addDataArr,NULL,mRealArr+i*fftLength,mImageArr+i*fftLength);
        }
        else{
            fftObj_fft(fftObj,_arr+i*slideLength,NULL,mRealArr+i*fftLength,mImageArr+i*fftLength);
        }
    }
    #endif
}

/***
	isPad =0
		dataLength>=fftLength
		t=(dataLength-fftLength)/slideLength+1 
	isPad =1
		dataLength>0
		t=(dataLength+fftLength-fftLength)/slideLength+1 ;padding fftLength
****/
static void __calTimeAndTailLen(int dataLength,int fftLength,int slideLength,int isPad,int *timeLength,int *tailLength){
	int timeLen=0;
	int tailLen=0;

	if(!isPad){ // 非填充
		timeLen=(dataLength-fftLength)/slideLength+1;
		tailLen=(dataLength-fftLength)%slideLength+(fftLength-slideLength);
	}
	else{
		timeLen=dataLength/slideLength+1;
		if(timeLen>1){ // padding is use tailLen
			tailLen=dataLength%slideLength;
		}
	}

	if(timeLength){
		*timeLength=timeLen;
	}

	if(tailLength){
		*tailLength=tailLen;
	}
}

void stftObj_debug(STFTObj stftObj){
	int fftLength=0;
	int slideLength=0;

	int timeLength=0; // x=timeLength

	fftLength=stftObj->fftLength;
	slideLength=stftObj->slideLength;

	timeLength=stftObj->timeLength;

	printf("stft params is: fftLength=%d, slideLength=%d, timeLength=%d\n",fftLength,slideLength,timeLength);
}

static int __isCOA(float *winArr,int winLength,int overlapLength){
	int flag=0;


	return flag;
}
















```

---

### Archivo: `./LICENSE.md`

```
## MIT License

Copyright (c) 2021--2024, `audioFlux` development team.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

### Archivo: `./README.md`

```
<img src='./image/logo.png'  width="400"  style="max-width: 100%;" > 

# audioFlux

<!-- shields.io -->
![GitHub Workflow Status (with branch)](https://img.shields.io/github/actions/workflow/status/libAudioFlux/audioFlux/build.yml?branch=master)
![example branch parameter](https://github.com/libAudioFlux/audioFlux/actions/workflows/build.yml/badge.svg?branch=master)
![language](https://img.shields.io/badge/language-C%20%7C%20Python%20-blue.svg)
[![PyPI - Version](https://img.shields.io/pypi/v/audioflux)](https://pypi.org/project/audioflux/)
[![PyPI - Python Version](https://img.shields.io/badge/python-%3E%3D3.6-brightgreen)](https://pypi.org/project/audioflux/)
[![Docs](https://img.shields.io/badge/Docs-passing-brightgreen)](https://audioflux.top/index.html)
![GitHub](https://img.shields.io/github/license/libAudioFlux/audioFlux)
<!--[![PyPI Downloads](https://img.shields.io/pypi/dm/audioflux.svg?label=Pypi%20downloads)](https://pypi.org/project/audioflux/)-->

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7548288.svg)](https://doi.org/10.5281/zenodo.7548288)

<!--[![codebeat badge](https://codebeat.co/badges/0e21a344-0928-4aee-8262-be9a41fa488b)](https://codebeat.co/projects/github-com-libaudioflux-audioflux-master)
![](https://img.shields.io/badge/pod-v0.1.1-blue.svg)-->


**`audioflux`** is a deep learning tool library for audio and music analysis, feature extraction. It supports dozens of
time-frequency analysis transformation methods and hundreds of corresponding time-domain and frequency-domain feature
combinations. It can be provided to deep learning networks for training, and is used to study various tasks in the audio
field such as Classification, Separation, Music Information Retrieval(MIR) and ASR etc.

<!-- **`audioflux`** has the following features: 
- Systematic and multi-dimensional feature extraction and combination can be flexibly used for various task research and analysis.
- High performance, core part C implementation, FFT hardware acceleration based on different platforms, convenient for large-scale data feature extraction.
- It supports the mobile end and meets the real-time calculation of audio stream at the mobile end. -->


##### New Features
* v0.1.8
  * Add a variety of Pitch algorithms: `YIN`, `CEP`, `PEF`, `NCF`, `HPS`, `LHS`, `STFT` and `FFP`.
  * Add `PitchShift` and `TimeStretch` algorithms.


### Table of Contents

- [Overview](#overview)
- [Installation](#installation)
    - [Python Package Install](#python-package-install)
    - [Other Build](#other-build)
- [Quickstart](#quickstart)
- [Benchmark](#benchmark)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [Citing](#citing)
- [License](#license)

## Overview

**`audioFlux`** is based on data stream design. It decouples each algorithm module in structure, and can quickly and
efficiently extract features of multiple dimensions. The following is the main feature architecture diagram.

<img src='./image/feature_all.png'>
<!--<img src='./feature_all.pdf'>-->

You can use multiple dimensional feature combinations, select different deep learning networks training, study various
tasks in the audio field such as Classification, Separation, MIR etc.

<img src='./image/flow.png'>


The main functions of **`audioFlux`** include **transform**, **feature** and **mir** modules.

#### 1. Transform

In the time–frequency representation, main transform algorithm:

- **`BFT`**&nbsp;&nbsp; - &nbsp;&nbsp;Based Fourier Transform, similar short-time Fourier transform.
- **`NSGT`** - &nbsp; Non-Stationary Gabor Transform.
- **`CWT`**&nbsp;&nbsp; - &nbsp;&nbsp;Continuous Wavelet Transform.
- **`PWT`**&nbsp;&nbsp; - &nbsp;&nbsp;Pseudo Wavelet Transform.

<!-- &emsp -->

The above transform supports all the following frequency scale types:

- Linear - Short-time Fourier transform spectrogram.
- Linspace - Linspace-scale spectrogram.
- Mel - Mel-scale spectrogram.
- Bark - Bark-scale spectrogram.
- Erb - Erb-scale spectrogram.
- Octave - Octave-scale spectrogram.
- Log - Logarithmic-scale spectrogram.

The following transform are not supports multiple frequency scale types, only used as independent transform:

- **`CQT`** - &nbsp;&nbsp;Constant-Q Transform.
- **`VQT`** - &nbsp;&nbsp;Variable-Q Transform.
- **`ST`**&nbsp;&nbsp; - &nbsp;&nbsp;S-Transform/Stockwell Transform.
- **`FST`** - &nbsp;&nbsp;Fast S-Transform.
- **`DWT`** - &nbsp;&nbsp;Discrete Wavelet Transform.
- **`WPT`** - &nbsp;&nbsp;Wave Packet Transform.
- **`SWT`** - &nbsp;&nbsp;Stationary Wavelet Transform.

Detailed transform function, description, and use view the documentation.

The *_synchrosqueezing_* or *_reassignment_* is a technique for sharpening a time-frequency representation, contains the
following algorithms:

- **`reassign`** - reassign transform for `STFT`.
- **`synsq`** - reassign data use `CWT` data.
- **`wsst`** - reassign transform for `CWT`.

#### 2. Feature

The feature module contains the following algorithms:

- **`spectral`** - Spectrum feature, supports all spectrum types.
- **`xxcc`** - Cepstrum coefficients, supports all spectrum types.
- **`deconv`** - Deconvolution for spectrum, supports all spectrum types.
- **`chroma`** - Chroma feature, only supports `CQT` spectrum, Linear/Octave spectrum based on `BFT`.

<!-- harmonic pitch class profiles(HPCP) -->

#### 3. MIR

The mir module contains the following algorithms:

- **`pitch`** - YIN, STFT, etc algorithm.
- **`onset`** - Spectrum flux, novelty, etc algorithm.
- **`hpss`** - Median filtering, NMF algorithm.

## Installation

![language](https://img.shields.io/badge/platform-%20Linux%20%7C%20macOS%20%7C%20Windows%20%7C%20iOS%20%7C%20Android%20-lyellow.svg)

The library is cross-platform and currently supports Linux, macOS, Windows, iOS and Android systems.

### Python Package Install

To install the **audioFlux** package, Python >=3.6, using the released python package.

Using PyPI:

```
$ pip install audioflux 
```

Using Anaconda:

```
$ conda install -c tanky25 -c conda-forge audioflux
```

<!--Read installation instructions:
https://audioflux.top/install-->

### Other Build

- [iOS build](docs/installing.md#ios-build)
- [Android build](docs/installing.md#android-build)
- [Building from source](docs/installing.md#building-from-source)

## Quickstart

- [Mel & MFCC](docs/examples.md#mel--mfcc)
- [CWT & Synchrosqueezing](docs/examples.md#cwt--synchrosqueezing)
- [CQT & Chroma](docs/examples.md#cqt--chroma)
- [Different Wavelet Type](docs/examples.md#different-wavelet-type)
- [Spectral Features](docs/examples.md#spectral-features)
- [Pitch Estimate](docs/examples.md#pitch-estimate)
- [Onset Detection](docs/examples.md#onset-detection)
- [Harmonic Percussive Source Separation](docs/examples.md#harmonic-percussive-source-separation)

More example scripts are provided in the [Documentation](https://audioflux.top/) section.

## Benchmark

server hardware:

    - CPU: AMD Ryzen Threadripper 3970X 32-Core Processor

<img src='./docs/image/benchmark/linux_amd_1.png' width="800" >

More detailed performance benchmark are provided in the [Benchmark](https://github.com/libAudioFlux/audioFlux/tree/master/benchmark) module.

## Documentation

Documentation of the package can be found online:

[https://audioflux.top](https://audioflux.top/)

## Contributing

We are more than happy to collaborate and receive your contributions to **`audioFlux`**. If you want to contribute,
please fork the latest git repository and create a feature branch. Submitted requests should pass all continuous
integration tests.

You are also more than welcome to suggest any improvements, including proposals for need help, find a bug, have a
feature request, ask a general question, new algorithms. <a href="https://github.com/libAudioFlux/audioFlux/issues/new">
Open an issue</a>

## Citing

If you want to cite **`audioFlux`** in a scholarly work, please use the following ways:

- If you are using the library for your work, for the sake of reproducibility, please cite the version you used as
  indexed at Zenodo:

  [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7548288.svg)](https://doi.org/10.5281/zenodo.7548288)

## License

audioFlux project is available MIT License.



```

---

