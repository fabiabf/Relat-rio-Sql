SELECT 	a.dt_aprovacao,
	a.dt_orcamento,
	a.dt_validade,
	NVL(a.nr_atendimento, :NR_ATENDIMENTO) nr_atendimento,
	a.qt_dia_internacao,
	a.qt_min_cc,
       	substr(OBTER_VALOR_DOMINIO(31, A.IE_STATUS_ORCAMENTO),1,254) DS_STATUS_ORCAMENTO,
       	substr(OBTER_NOME_CONVENIO(A.CD_CONVENIO),1,254)  DS_CONVENIO,
       	C.DS_CATEGORIA,
       	D.DS_CONDICAO_PAGAMENTO,
       	E.NM_PESSOA_FISICA,
	substr(obter_descricao_padrao('TIPO_ACOMODACAO','DS_TIPO_ACOMODACAO', a.cd_tipo_acomodacao),1,254) ds_tipo_acomodacao,
	substr(obter_valor_dominio(1909, a.ie_tipo_orcamento),1,150) ds_tipo_orcamento
FROM 	CONDICAO_PAGAMENTO D,
	CATEGORIA_CONVENIO C,
     	PESSOA_FISICA E,
	ORCAMENTO_PACIENTE A
WHERE  	A.NR_SEQUENCIA_ORCAMENTO  	= :NR_SEQUENCIA_ORCAMENTO
  AND 	A.CD_CATEGORIA   		= C.CD_CATEGORIA
  AND 	A.CD_CONVENIO			= C.CD_CONVENIO
  AND 	A.CD_CONDICAO_PAGAMENTO   	= D.CD_CONDICAO_PAGAMENTO
  AND 	A.CD_PESSOA_FISICA         		= E.CD_PESSOA_FISICA
