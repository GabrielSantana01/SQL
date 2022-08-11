# SQL

-- isso seria uma contador que rodaria em uma job de tempo em tempo no intuito de verificar se o valor de uma tabela esta sendo replicado no backup

declare @increId int;
declare @ultId int;
 
select @ultLeitura = (SELECT TOP 1 contador FROM [Integracao].[dbo].[contador] order by id desc)
select @increCont = @ultLeitura + 60;

select @ultId = (SELECT TOP 1 id FROM [Integracao].[dbo].[contador] order by id desc)
select @increId = @ultId + 1;
--insert into [Integracao].[dbo].[contador] Values(1, SYSDATETIME(), 1)
insert into [Integracao].[dbo].[contador] Values(@increId, SYSDATETIME(), @increCont)

delete [Integracao].[dbo].[contador] where id = @ultId
