# Lista 5 - Normalização

## Exercício 1

-> Código `sql`base:
```sql
-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema Exerc1NormOriginal
CREATE SCHEMA Exerc1NormOriginal;

USE Exerc1NormOriginal;
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Table `ItemPedido`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `ItemPedido` (
  `numPedido` INT NOT NULL,
  `codProduto` CHAR(10) NOT NULL,
  `qtdePedida` DECIMAL(4) NOT NULL,
  `dataPedido` DATE NOT NULL,
  `codCliente` INT NOT NULL,
  `nomeCliente` VARCHAR(50) NOT NULL,
  `codVendedor` INT NOT NULL,
  `nomeVendedor` VARCHAR(50) NOT NULL,
  `descricaoProduto` VARCHAR(100) NOT NULL,
  `precoVendaProduto` DECIMAL(8,2) NOT NULL,
  PRIMARY KEY (`numPedido`, `codProduto`))
ENGINE = InnoDB;

INSERT INTO ItemPedido VALUES (1,'AAA',2,'2023-10-02',100,'Cliente João',50,'Vendedora Maria','Teclado',60);
INSERT INTO ItemPedido VALUES (1,'BBB',3,'2023-10-02',100,'Cliente João',50,'Vendedora Maria','Mouse',40);
INSERT INTO ItemPedido VALUES (2,'BBB',5,'2023-10-03',200,'Cliente Ana', 50,'Vendedora Maria','Mouse',40);
INSERT INTO ItemPedido VALUES (2,'CCC',1,'2023-10-03',200,'Cliente Ana', 50,'Vendedora Maria','Monitor',450);
INSERT INTO ItemPedido VALUES (3,'AAA',1,'2023-10-03',100,'Cliente João',60,'Vendedor Pedro','Teclado',60);
INSERT INTO ItemPedido VALUES (4,'AAA',3,'2023-10-04',200,'Cliente Ana', 60,'Vendedor Pedro','Teclado',60);

-- -----------------------------------------------------
-- Schema Exerc1Norm2FN
CREATE SCHEMA Exerc1Norm2FN;

USE Exerc1Norm2FN;
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Table `Pedido`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Pedido` (
  `numPedido` INT NOT NULL,
  `dataPedido` DATE NOT NULL,
  `codCliente` INT NOT NULL,
  `nomeCliente` VARCHAR(50) NOT NULL,
  `codVendedor` INT NOT NULL,
  `nomeVendedor` VARCHAR(50) NOT NULL,
  PRIMARY KEY (`numPedido`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Produto`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Produto` (
  `codProduto` CHAR(10) NOT NULL,
  `descricaoProduto` VARCHAR(100) NOT NULL,
  `precoVendaProduto` DECIMAL(8,2) NOT NULL,
  PRIMARY KEY (`codProduto`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `ItemPedido`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `ItemPedido` (
  `numPedido` INT NOT NULL,
  `codProduto` CHAR(10) NOT NULL,
  `qtdePedida` DECIMAL(4) NOT NULL,
  PRIMARY KEY (`numPedido`, `codProduto`),
  INDEX `fk_Pedido_has_Produto_Produto1_idx` (`codProduto` ASC),
  INDEX `fk_Pedido_has_Produto_Pedido_idx` (`numPedido` ASC),
  CONSTRAINT `fk_Pedido_has_Produto_Pedido`
    FOREIGN KEY (`numPedido`)
    REFERENCES `Pedido` (`numPedido`)
    ON DELETE CASCADE
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Pedido_has_Produto_Produto1`
    FOREIGN KEY (`codProduto`)
    REFERENCES `Produto` (`codProduto`)
    ON DELETE CASCADE
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

INSERT INTO Pedido VALUES (1,'2023-10-02',100,'Cliente João',50,'Vendedora Maria');
INSERT INTO Pedido VALUES (2,'2023-10-03',200,'Cliente Ana', 50,'Vendedora Maria');
INSERT INTO Pedido VALUES (3,'2023-10-03',100,'Cliente João',60,'Vendedor Pedro');
INSERT INTO Pedido VALUES (4,'2023-10-04',200,'Cliente Ana', 60,'Vendedor Pedro');

INSERT INTO Produto VALUES ('AAA','Teclado',60);
INSERT INTO Produto VALUES ('BBB','Mouse',40);
INSERT INTO Produto VALUES ('CCC','Monitor',450);

INSERT INTO ItemPedido VALUES (1,'AAA',2);
INSERT INTO ItemPedido VALUES (1,'BBB',3);
INSERT INTO ItemPedido VALUES (2,'BBB',5);
INSERT INTO ItemPedido VALUES (2,'CCC',1);
INSERT INTO ItemPedido VALUES (3,'AAA',1);
INSERT INTO ItemPedido VALUES (4,'AAA',3);

-- -----------------------------------------------------
-- Schema Exerc1Norm3FN
CREATE SCHEMA Exerc1Norm3FN;

USE Exerc1Norm3FN;
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Table `Cliente`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Cliente` (
  `codCliente` INT NOT NULL,
  `nomeCliente` VARCHAR(50) NOT NULL,
  PRIMARY KEY (`codCliente`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Vendedor`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Vendedor` (
  `codVendedor` INT NOT NULL,
  `nomeVendedor` VARCHAR(50) NOT NULL,
  PRIMARY KEY (`codVendedor`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Pedido`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Pedido` (
  `numPedido` INT NOT NULL,
  `dataPedido` DATE NOT NULL,
  `codCliente` INT NOT NULL,
  `codVendedor` INT NOT NULL,
  PRIMARY KEY (`numPedido`),
  INDEX `fk_Pedido_Cliente1_idx` (`codCliente` ASC),
  INDEX `fk_Pedido_Vendedor1_idx` (`codVendedor` ASC),
  CONSTRAINT `fk_Pedido_Cliente1`
    FOREIGN KEY (`codCliente`)
    REFERENCES `Cliente` (`codCliente`)
    ON DELETE RESTRICT
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Pedido_Vendedor1`
    FOREIGN KEY (`codVendedor`)
    REFERENCES `Vendedor` (`codVendedor`)
    ON DELETE RESTRICT
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `Produto`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `Produto` (
  `codProduto` CHAR(10) NOT NULL,
  `descricaoProduto` VARCHAR(100) NOT NULL,
  `precoVendaProduto` DECIMAL(8,2) NOT NULL,
  PRIMARY KEY (`codProduto`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `ItemPedido`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `ItemPedido` (
  `numPedido` INT NOT NULL,
  `codProduto` CHAR(10) NOT NULL,
  `qtdePedida` DECIMAL(4) NOT NULL,
  PRIMARY KEY (`numPedido`, `codProduto`),
  INDEX `fk_Pedido_has_Produto_Produto2_idx` (`codProduto` ASC),
  INDEX `fk_Pedido_has_Produto_Pedido1_idx` (`numPedido` ASC),
  CONSTRAINT `fk_Pedido_has_Produto_Pedido1`
    FOREIGN KEY (`numPedido`)
    REFERENCES `Pedido` (`numPedido`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_Pedido_has_Produto_Produto2`
    FOREIGN KEY (`codProduto`)
    REFERENCES `Produto` (`codProduto`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;

INSERT INTO Cliente VALUES (100,'Cliente João');
INSERT INTO Cliente VALUES (200,'Cliente Ana');

INSERT INTO Vendedor VALUES (50,'Vendedora Maria');
INSERT INTO Vendedor VALUES (60,'Vendedor Pedro');

INSERT INTO Pedido VALUES (1,'2023-10-02',100,50);
INSERT INTO Pedido VALUES (2,'2023-10-03',200,50);
INSERT INTO Pedido VALUES (3,'2023-10-03',100,60);
INSERT INTO Pedido VALUES (4,'2023-10-04',200,60);

INSERT INTO Produto VALUES ('AAA','Teclado',60);
INSERT INTO Produto VALUES ('BBB','Mouse',40);
INSERT INTO Produto VALUES ('CCC','Monitor',450);

INSERT INTO ItemPedido VALUES (1,'AAA',2);
INSERT INTO ItemPedido VALUES (1,'BBB',3);
INSERT INTO ItemPedido VALUES (2,'BBB',5);
INSERT INTO ItemPedido VALUES (2,'CCC',1);
INSERT INTO ItemPedido VALUES (3,'AAA',1);
INSERT INTO ItemPedido VALUES (4,'AAA',3);

SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
```
**Resumo**: ItemPedido (numPedido, codProduto, qtdePedida, dataPedido, codCliente,
nomeCliente, codVendedor, nomeVendedor, descricaoProduto, precoVendaProduto).

Já está na 1FN, preciso passar para a 2FN.

[*Upload* do exercício 1, letra A](https://imgur.com/a/i5r3F5f).

Agora, passando da 2FN para a 3FN...

[*Upload* do exercício 1, letra B](https://imgur.com/YSqImoO).
