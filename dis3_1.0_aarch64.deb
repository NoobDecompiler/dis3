# Codex By KangEhem
# Udah Tinggal pake aja, gak usah di recode:v
import re
import sys
import os
import marshal
import zlib
import base64
import types
import time
import struct
import io
from opcode import *
if sys.version_info >= (3,4):
        from importlib.util import MAGIC_NUMBER
else:
    import imp
    MAGIC_NUMBER = imp.get_magic()
kapten=base64.b64decode(b'PFRoaXMgQ29kZSBHZW5lcmF0ZWQgQnkgRGlzMz4=').decode()

def _pack_uint32(val):
    return struct.pack("<I", val)

def code_to_bytecode(code, mtime=0, source_size=0):
    data = bytearray(MAGIC_NUMBER)
    if sys.version_info >= (3,7):
        data.extend(_pack_uint32(0))
    data.extend(_pack_uint32(int(mtime)))
    if sys.version_info >= (3,2):
        data.extend(_pack_uint32(source_size))
    data.extend(marshal.dumps(code))
    return data

def dump_to_pyc(byte_code, file):
    pyc_code = code_to_bytecode(byte_code, time.time())
    with open(file, mode="wb") as f:
        f.write(pyc_code)

class Asm:
    def __init__(self, file, ki=False):
        self.file=file
        self.ki=ki
        self.mm=lambda x:bytes(bytearray(x))

    def kawai(self,c,b,a):
        c1 = c.co_code
        c2 = c.co_consts
        if a in [1]:
            c1=b
        if a in [2]:
            c2=b
        data=[c.co_argcount,c.co_nlocals,c.co_stacksize,c.co_flags,c1,c2,c.co_names,c.co_varnames,c.co_filename,c.co_name,c.co_firstlineno,c.co_lnotab,c.co_freevars,c.co_cellvars]
        try:
            data[1:1] = [c.co_posonlyargcount,c.co_kwonlyargcount]
        except:
            data.insert(1, c.co_kwonlyargcount)
        return types.CodeType(*data)

    def get_byte_code(self, source):
        s = re.findall("\((.*)\)", source)[0]
        xs = "".join([chr(int(i)) for i in s.split(",")])
        return marshal.loads(zlib.decompress(base64.b64decode(xs)))

    def regex(self, rb, line=''):
        obj = []
        split = rb.splitlines()
        i = 0
        while i < len(split):
            x = split
            if x[i].startswith(line):
                i = i+1
                continue
            s = x[i].split()
            wtf = len(s)
            for y in range(wtf):
                if s[y] in opmap.keys():
                    obj.append(opmap[s[y]])
                    obj.append(int(s[y+1]))
                    break
            i = i+1
        return obj

    def main_asm(self):
        read = open(self.file).read().split(kapten)
        module = self.get_byte_code(read[0])
        load_const = list(module.co_consts)
        ln = len(read)-1
        arg_repr = 0
        while arg_repr < ln:
            sc = read[arg_repr]
            su = sc.splitlines()
            if "const" and "<code object" in str(su):
                k = re.findall("\((\d+)\)", str(su[1]))
                ajg = len(k)
                if ajg in [1]:
                    i = int(k[0])
                    xx=load_const[i]
                    z = self.regex(sc, "const")
                    kode=self.mm(z)
                    load_const[i] = self.kawai(xx,kode,1)
                if ajg in [2]:
                    a = int(k[0])
                    b = int(k[1])
                    xz = load_const[a]
                    zx = list(xz.co_consts)
                    cs = zx[b]
                    sb = self.regex(sc, "const")
                    kode = self.mm(sb)
                    zx[b] = self.kawai(cs,kode,1)
                    load_const[a] = self.kawai(xz,tuple(zx),2)
            arg_repr = arg_repr+1
        ab = self.regex(read[1], "module")
        kode = self.mm(ab)
        xw = self.kawai(module, kode, 1)
        return self.kawai(xw, tuple(load_const), 2)

    def main(self):
        byte_code = self.main_asm()
        if self.ki:
            return byte_code
        pyc_file = ".".join([os.path.splitext(self.file)[0], "pyc"])
        dump_to_pyc(byte_code, pyc_file)
        print("sukses write to %s" % pyc_file)

class Dis:
    def __init__(self,code):
        self.kodek=code

    def dis_py3(self, code):
        aray = code.co_code
        argval = list(aray)
        i = 0
        x = code
        ln = len(argval)-1
        while i < ln:
            oparg = argval[i]
            op = opname[oparg]
            arg = argval[i+1]
            ajg=" ".join(["", repr(i), op, repr(arg)])
            if oparg in hasname:
                print("%s (%s)"%(ajg, x.co_names[arg]))
            elif oparg in haslocal:
                print("%s (%s)"%(ajg, x.co_varnames[arg]))
            elif oparg in hasconst:
                print("%s (%s)"%(ajg, repr(x.co_consts[arg])))
            elif oparg in hascompare:
                print("%s (%s)"%(ajg, cmp_op[arg]))
            else:print(ajg)
            i = i+2
        print(kapten)

    def puki(self,y,z):
        print(y)
        self.dis_py3(z)

    def try1(self,x,y=None):
        ln = len(x)
        for i in range(ln):
            arg = x[i]
            if type(arg) is types.CodeType:
                self.puki(y%(str(i), str(arg)),arg)
                self.try1(arg.co_consts, "const ("+str(i)+")(%s) %s")

    def main(self):
        print("# This Script Written By KangEhem")
        print("# Dont Forget To Follow My Github Profile !")
        ag=base64.b64encode(zlib.compress(marshal.dumps(self.kodek)))
        byte=list(ag)
        list_byte = '(%s)'%','.join([str(i) for i in byte])
        self.puki('%s\n%s\nmodule %s '%(list_byte,kapten,str(self.kodek)), self.kodek)
        self.try1(self.kodek.co_consts, "const (%s) %s")

def load_module(fk):
    y = None
    try:
        x = open(fk).read()
        y = compile(x,fk,"exec")
    except Exception as i:
        try:
            f = open(fk, "rb")
            f.seek(16)
            y = marshal.loads(f.read())
        except Exception as i:
            exit("Sepertinya ada kesalahan di file %s"%fk)
    return y

def cekfile(f):
    if not os.path.exists(f):
        exit("File %s Tidak Ditemukan"%f)

def menu(sys):
    asm = False
    if len(sys) <= 2:
        exit("usage: dis3 (dis|asm) file.py")
    file = sys[2]
    if sys[1] == "asm":
        asm = True
    cekfile(file)
    if asm:
        Asm(file).main()
    else:
        x = load_module(file)
        Dis(x).main()

def main():
    try:menu(sys.argv)
    except (KeyboardInterrupt, EOFError):exit()
# Mau Nyari Apaan Sih Cuk?