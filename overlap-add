import numpy as np
import math
def circonv(x,y):
    g=np.array(x)
    h=np.array(y)
    if g.size != h.size:
        raise Exception("Sequences not of same length")
    N = g.size 
    htr=np.concatenate([[h[0]], h[:0:-1]])
    y=np.zeros(N)
    for n in np.arange(N):
        y[n]=np.sum(g*htr)
        htr=np.roll(htr,1)
    Y=y.tolist()
    return Y
def oa(sig,imp):
    M=len(imp)
    N=len(sig)+1
    L=N-M+1
    h=imp+[0]*(L-1)
    x_block=[0]*N
    i=0
    j=0
    count=0
    while i<len(sig):
        i=(j+1)*L
        j=j+1
        count=count+1
    conv_mat=[]
    i=0
    j=0
    while i<len(sig):
        x_block=sig[i:((j+1)*L)]+[0]*(M-1)
        if len(x_block)!=len(sig)+1:
            x_block=x_block+[0]*(len(sig)+1-len(x_block))
        i=(j+1)*L
        y_block=circonv(x_block,h)
        conv_mat.append(y_block)
        j=j+1
    Y=[]
    k=0
    mid_block=[0]*(M-1)
    midblock_mat=[]
    while k+1<count:
        temp1=conv_mat[k]
        temp2=conv_mat[k+1]
        for l in range(M-1):
            mid_block[l]=temp1[N-M+1+l]+temp2[l]
        midblock_mat.append(mid_block)
        k=k+1
    for m in range(count):
        mat1=conv_mat[m]
        temp1=mat1
        if m==0:
            mat2=midblock_mat[m]
            temp2=mat2
            temp3=temp1[:N-M+1]+temp2
            Y=Y+temp3
        elif m==count-1:
            temp3=temp1[M-1:]
            Y=Y+temp3
        else:
            mat2=midblock_mat[m]
            temp2=mat2
            temp3=temp1[M-1:N-M+1]+temp2
            Y=Y+temp3
    return Y[:len(sig)+M-1]
sig1=[1,2,3,3,2,1,-1,-2,-3,5,6,-1,2,0,2,1] #input signal
imp1=[3,2,1,1] #input impulse
print(oa(sig1,imp1))    
