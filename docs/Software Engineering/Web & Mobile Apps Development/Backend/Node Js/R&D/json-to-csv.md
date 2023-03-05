## json to csv in nodejs

```jsx showLineNumbers
import { parse } from 'json2csv';
import * as fs from 'fs';


public async generateDailyEFUContractCsv(
    prisma: PrismaClient = null,
  ): Promise<Contract[]> {
    if (prisma == null) {
      prisma = this.prisma;
    }

    const yesterdayUTCDate = moment().subtract(1, 'days').utc().format();
    this.logger.debug(`yesterdayUTCDate, ${yesterdayUTCDate}`);

    const contracts = await prisma.contract.findMany({
      where: {
        takafulId: 4,
        createdAt: {
          gte: yesterdayUTCDate, //fetching records made in last 24 hours
        },
      },
      orderBy: {
        createdAt: 'asc',
      },
      include: {
        TakafulContract: {
          select: {
            takafulContractCode: true,
            takafulContractId: true,
            takafulContractUrl: true,
          },
        },
      },
    });
    this.logger.debug(`contracts?.length : ${contracts?.length}, contracts: ${JSON.stringify(contracts)}`);

    if (contracts?.length > 0) {
      for (let i = 0; i < contracts?.length; i++) {
        const contract = contracts[i];

        // const myData = json.car;
        const myData = [...contracts];
        // const fields = ['name', 'price', 'color', 'nestedobject'];
        // const opts = { fields };
        // const csv = parse(myData, opts);
        const csv = parse(myData);

        // fs.writeFile('./src/contract/efu-contracts.csv', csv, function (err) {
        //   if (err) throw err;
        //   console.log('Efu contracts file saved');
        // });

        const context: ServiceContext = {
          user: await this.common.getUser(contract.createdBy),
        };

        const attachments = [
          {
            filename: 'efu-contracts.csv',
            content: csv,
          },
        ];

        await this.notifiction.sendMessageToPerson(
          context,
          `contract-generated`,
          `Hefazat Contract - ${contract.contractNumber} - Type ${contract.hefazatProductTypeId}`,
          {
            name: contract.customerName,
            contractNumber: contract.contractNumber,
            product: contract.productSku,
            certificateUrl: this.getContractCertificateUrl(contract),
            tccUrl: this.common.getContractTCCUrl(contract),
            cussappUrl: this.common.getCustomerAppUrl(MobilePlatform.Android),
            contractType: contract.hefazatProductTypeId,
          },
          contract.customerEmail,
          contract.customerMobile,
          attachments
        );
      }
    }

    this.logger.warn('line break\n\n\n\n\n');
    return contracts;
  }
}
```

https://stackoverflow.com/questions/49006544/json2csv-is-not-a-function-in-nodejs
