# -image-compressor

from tkinter import *
from PIL import Image
from tkinter.filedialog import *

#definindo cores
cor0 = "#000000"  # black
cor6 = "#d9d9d9"  # grey
cor7 = "#f5d105"  #yellow

janela = Tk()
janela.geometry('430x250')
janela.title('Compressor de imagem')
janela.configure(bg=cor0)
janela.resizable(width=False, height=False)

#definindo frame
frame = Frame(janela,width=420,height=250,bg=cor0,relief='flat')
frame.grid(row=0,column=0,sticky='nsew')

app_name = Label(frame,text='Compressor de imagem',width=29,height=1,anchor=CENTER,relief='flat',
                 font='Helvetica 18 bold',fg=cor7,bg=cor0)
app_name.grid(row=0,column=0,sticky=NSEW,columnspan=2,pady=1)

# para abrir um novo arquivo
def novo_arquivo():
 # Abrindo imagem
    ficheiro = askopenfilename()
    img = Image.open(ficheiro)
    img_rgb = img.convert('RGB')

    # tamanho da imagem original
    img_altura, img_largura = img.size

    def converter():
        # novas medidas
        altura = int(entry_altura.get())
        largura = int(entry_largura.get())

        novo_valor= (altura, largura)
        nova_imagem = img_rgb.resize(novo_valor)

        img_salvar = asksaveasfilename()

        nova_imagem.save(img_salvar + '.JPG')


    tamanho_original= Label(frame, text='Largura e Altura original ' + str(img_altura)+'x' + str(img_largura) + 'px',
                            width=24, height=1, anchor=CENTER, relief='flat',font='Helvetica 10 bold', fg=cor6, bg=cor0)
    tamanho_original.grid(row=2, column=0, sticky=NSEW, columnspan=2, pady=1)

    # definindo caixa de entrada
    nova_altura = Label(frame, text='Digite nova altura', width=24, height=1, anchor=CENTER, padx=10, pady=7,
                        relief='flat',font='Helvetica 10 bold', fg=cor7, bg=cor0)
    nova_altura.grid(row=3, column=0, sticky=NSEW, pady=5)

    nova_largura = Label(frame, text='Digite nova largura', width=24, height=1, anchor=CENTER, padx=10, pady=7,
                         relief='flat',font='Helvetica 10 bold', fg=cor7, bg=cor0)
    nova_largura.grid(row=3, column=1, sticky=NSEW, pady=5)

    entry_altura = Entry(frame, width=9, justify='center', bg=cor6)
    entry_altura.grid(row=4, column=0, sticky=NSEW, pady=5)

    entry_largura = Entry(frame, width=9, justify='center', bg=cor6)
    entry_largura.grid(row=4, column=1, sticky=NSEW, pady=5)

    # definindo botao converter
    b_convert = Button(frame, text='Converter', font='4', width=10, height=1,
                       anchor=CENTER, relief=RAISED, fg=cor0, bg=cor7, overrelief=RIDGE,command=converter)

    b_convert.grid(row=5, column=0, columnspan=2, padx=0, pady=5)

# botao selecionar imagem
b_novo = Button(frame,text='+ Selecionar imagem',font='4',width=47,height=1,
                anchor=CENTER,relief=RAISED, fg=cor0,bg=cor7,overrelief=RIDGE, command=novo_arquivo)
b_novo.grid(row=1,column=0,sticky=EW,columnspan=4,pady=1)

janela.mainloop()
