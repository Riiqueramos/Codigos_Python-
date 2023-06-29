from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.common.action_chains import ActionChains

import pandas as pd
import openpyxl
import time
import requests

#1 Inicializar o driver do navegador
browser = webdriver.Chrome()

#2 Abrir a página desejada
browser.get("https://bi.sequoialog.com.br")

#3 Maximizar o site
browser.maximize_window()
time.sleep(5)

#4 Encontrar o campo de usuário e digitar o usuário
campo_usuario = browser.find_element(By.XPATH, "//*[@data-tb-test-id='username-TextInput']")
campo_usuario.send_keys("indicadores.bi")
time.sleep(3)

#5 Encontrar o campo de senha e digitar a senha
campo_senha = browser.find_element(By.XPATH, "//*[@data-tb-test-id='password-TextInput']")
campo_senha.send_keys("mudar123")
time.sleep(3)

#6 Clicar no botão de login
botao_login = browser.find_element(By.XPATH, "//*[@data-tb-test-id='username-and-password-submit-Button']")
botao_login.click()
time.sleep(10)

#7 Acessar segmento B2B Pesado
botao_pesado = browser.find_element(By.XPATH, "//*[@data-tb-test-id='list-item-B2B e Pesados']")
botao_pesado.click()
time.sleep(4)

#8 Clicar no Explorar
botao_explora = browser.find_element(By.XPATH, "//*[@data-tb-test-id='top-nav-site-content']")
botao_explora.click()
time.sleep(4)

#9 Clicar no Pesado
site_pesado = browser.find_element(By.XPATH, "//*[@href='/#/site/B2BePesados/projects/88']")
site_pesado.click()
time.sleep(4)

#10 Clicar no Painel SSW
painel_ssw = browser.find_element(By.XPATH, "//*[@title='Painéis SSW']")
painel_ssw.click()
time.sleep(4)

#11 Clicar no SLA Gestão Cliente
painel_sla = browser.find_element(By.XPATH, "//*[@title='SLA - Gestão cliente']")
painel_sla.click()
time.sleep(9)

#12 Encontre o elemento da imagem usando um seletor (por exemplo, seletor CSS ou XPath)
imagem_elemento = browser.find_element_by_css_selector("//*[@data-tb-test-id='VisualizationScrollContainer'][@style='cursor: default; user-select: none; -webkit-tap-highlight-color: transparent; left: 0px; top: 0px; width: 133px; height: 31px;']")

#13 Obtenha o atributo 'src' da imagem
imagem_url = imagem_elemento.get_attribute("src='/vizql/tilecache/FE30395A9AB84AD4B2E1967456A379CA-1:1/8302/b2966e88b68e31d3a4e7ea3e60f6033991d31f4b3e54ec4ff91cb9a38f1be9f9/views.11712995244227850845_2482612563889942860.viz.0.0.png?=1688049557264Z2'")

#14 Use bibliotecas como requests ou urllib para baixar a imagem
nome_arquivo = "dt_carga.jpg"
caminho_salvar = "C:/Users/henrique.brito/Desktop/Data Carga" + nome_arquivo
response = requests.get(imagem_url)
with open(caminho_salvar, "wb") as arquivo:
    arquivo.write(response.content)

# Fechar o navegador
browser.quit()
