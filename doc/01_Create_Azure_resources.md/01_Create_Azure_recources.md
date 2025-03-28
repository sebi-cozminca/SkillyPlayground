---
title: 'Exercise 01: Create Azure resources'
layout: default
nav_order: 2
has_children: true
---

# @lab.Title 

## Introduction  

The City of Metropolis is dedicated to enhancing public services and administrative efficiency to meet the growing demands of its citizens. Faced with outdated document management systems and time-consuming administrative tasks, the city has embarked on a digital transformation journey. By migrating their on-premises PostgreSQL server to Azure Database for PostgreSQL, the City of Metropolis aims to streamline operations, improve data management, and deliver faster, more efficient public services.

During this lab, you'll learn how to set up the necessary prerequisites and perform the migration of an on-premises PostgreSQL server to Azure Database for PostgreSQL. You'll be performing both an offline and online migration of the Adventureworks sample database, mirroring the city's strategy to modernize its administrative infrastructure.

## Objectives  

After completing this lab, you'll be able to:  

- Create an Azure Database for PostgreSQL server in Azure. 
- Create a virtual network, gateway, and VPN connection in Azure. 

## Estimated Time  

30 minutes 

## Connection Instructions 

1. Connect to the virtual machine using the following credentials: 

    | Item | Value |
    |:--------|:--------|
    | Username   | **@lab.VirtualMachine(WindowsClientPostgreSQL16).Username**   |  
    | Password  | **@lab.VirtualMachine(WindowsClientPostgreSQL16).Password** |

    {: .highlight } 
    > Select the **Type Text** icon to enter the associated text into the virtual machine. 

1. Change the screen resolution if required. 

    {: .highlight } 
    > You may want to adjust the screen resolution to your own preference. Do this by right-clicking on the desktop and choosing **Screen resolution** and selecting **OK** when finished. 
