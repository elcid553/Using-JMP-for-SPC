names default to here(1);
dt2 = Open( "C:\Users\nxf73417\OneDrive - NXP\thk_limits.jmp");
dt = Open( "C:\Users\nxf73417\OneDrive - NXP\ox_spc.txt");

New Window("Input", <<Modal,  //creates pop-up window
	H List box( Text Box("Input Recipe"), recipeName = Text Edit Box()),  //type in desired recipe
	Button Box("OK",
		Recipe = recipeName << get text;
		dt2 << select where(dt2:PROCESS == Recipe); //filters thickness limits to desired recipe
		dtSubset = dt2 << subset(selected columns(0), selected rows(1));
		dt << select where(dt:process != Recipe);  //filters raw SPC data down to desired recipe
		dt << delete rows;
		
	)
);

//Pulls limit from new dt created from dt2
ucl = Column(dtSubset, "uclx")[1];
ucl = Column(dtSubset, "uclx")[1];
ct = Column(dtSubset, "mean")[1];
lcl = Column(dtSubset, "lclx")[1];
std = Column(dtSubset, "S_UCL")[1];
inc = ucl - ct;
mx = ucl + ucl*0.03;  //give different name, max and min are function names
mn = lcl - lcl*0.03;
std_max = std*1.7;

//Change run date to desired format
dt:stop << datatype(numeric)<<modelingtype(continuous)<<Format("m/d/y");

//Change load size data type
dt:outnote << data type(character);

//Delete excess columns
dt << Delete Columns(:comment,
	:moddate,
	:MODUSER,
	:opstart,
	:opstop,
	:THICK P1UNIT1,
	:THICK P1UNIT2,
	:THICK P1UNIT3,
	:THICK P1UNIT4,
	:THICK P1UNIT5,
	:THICK P1U4L1,
	:THICK P1U4L2,
	:THICK P1U4L3,
	:THICK P1U4L4,
	:THICK P1U4L5,
	:THICK P1U4L6,
	:THICK P1U4L7,
	:THICK P1U4L8,
	:THICK P1U4L9,
	:THICK P1U5L1,
	:THICK P1U5L2,
	:THICK P1U5L3,
	:THICK P1U5L4,
	:THICK P1U5L5,
	:THICK P1U5L6,
	:THICK P1U5L7,
	:THICK P1U5L8,
	:THICK P1U5L9,
	:DUMMY P2RSLTX,
	:DUMMY P2UNIT1,
	:DUMMY P2U1L1,
	:OVERLAY P3RSLTX,
	:OVERLAY P3UNIT1,
	:OVERLAY P3UNIT2,
	:OVERLAY P3U1L1,
	:OVERLAY P3U2L1,
	:DELTATOX P5RSLTX,
	:DELTATOX P5UNIT1,
	:DELTATOX P5UNIT2,
	:DELTATOX P5U1L1,
	:DELTATOX P5U1L2,
	:DELTATOX P5U1L3,
	:DELTATOX P5U1L4,
	:DELTATOX P5U1L5,
	:DELTATOX P5U1L6,
	:DELTATOX P5U1L7,
	:DELTATOX P5U1L8,
	:DELTATOX P5U1L9,
	:DELTATOX P5U2L1,
	:DELTATOX P5U2L2,
	:DELTATOX P5U2L3,
	:DELTATOX P5U2L4,
	:DELTATOX P5U2L5,
	:DELTATOX P5U2L6,
	:DELTATOX P5U2L7,
	:DELTATOX P5U2L8,
	:DELTATOX P5U2L9,
	:GOF P6U4L1,
	:GOF P6U4L2,
	:GOF P6U4L3,
	:GOF P6U4L4,
	:GOF P6U4L5,
	:GOF P6U4L6,
	:GOF P6U4L7,
	:GOF P6U4L8,
	:GOF P6U4L9,
	:GOF P6U5L1,
	:GOF P6U5L2,
	:GOF P6U5L3,
	:GOF P6U5L4,
	:GOF P6UNIT1,
	:GOF P6UNIT2,
	:GOF P6UNIT3,
	:GOF P6UNIT4,
	:GOF P6UNIT5,
	:GOF P6U5L5,
	:GOF P6U5L6,
	:GOF P6U5L7,
	:GOF P6U5L8,
	:GOF P6U5L9,
	:COMMENT1,
	:COMMENT2,
	:COMMENT3,
	:COMMENT4,
	:COMMENT5,
	:PRECIPE,
	:PTABLE,
	:LPATTERN,
	:LSLOT4,
	:LSLOT5,
	:WID4,
	:WID5,
	:PREA1,
	:PREA2,
	:PREA3,
	:PREA4,
	:PREA5,
	:PRET1,
	:PRET2,
	:PRET3,
	:PRET4,
	:PRET5,
	:POSA1,
	:POSA2,
	:POSA3,
	:POSA4,
	:POSA5,
	:POST1,
	:POST2,
	:POST3,
	:POST4,
	:POST5,
	:AX,
	:AR,
	:TX,
	:TR,
	:pretox4,
	:pretox5,
	:TP41,
	:TP42,
	:TP43,
	:TP44,
	:TP45,
	:TP46,
	:TP47,
	:TP48,
	:TP49,
	:BP41,
	:BP42,
	:BP43,
	:BP44,
	:BP45,
	:BP46,
	:BP47,
	:BP48,
	:BP49,
	:BT41,
	:BT42,
	:BT43,
	:BT44,
	:BT45,
	:BT46,
	:BT47,
	:BT48,
	:BT49,
	:BT51,
	:BT52,
	:BT53,
	:BT54,
	:BT55,
	:BT56,
	:BT57,
	:BT58,
	:BT59,
	:TP51,
	:TP52,
	:TP52,
	:TP53,
	:TP54,
	:TP55,
	:TP56,
	:TP57,
	:TP58,
	:TP59,
	:BP51,
	:BP52,
	:BP53,
	:BP54,
	:BP55,
	:BP56,
	:BP57,
	:BP58,
	:BP59,
	:HOUR_NEW,
	:MIN_NEW,
	:SEC_NEW,
	:TIMEWHO,
	:TEMPWHO,
	:FLOWWHO,
	:TIMECHNG,
	:FLOWCHNG,
	:TEMPCHNG,
	:FLOWOLD,
	:FLOWNEW,
	:LINKWHO,
	:TIMELINK,
	:OXRATE P4UNIT1,
	:t_new,
	:tc_new,
	:c_new,
	:bc_new,
	:b_new,
	:HOUR_OLD,
	:MIN_OLD,
	:SEC_OLD,
	:THICK,
	:TSLOT41,
	:TSLOT42,
	:TSLOT43,
	:TSLOT44,
	:TSLOT45,
	:TSLOT46,
	:TSLOT47,
	:TSLOT48,
	:TSLOT49,
	:TSLOT51,
	:TSLOT52,
	:TSLOT53,
	:TSLOT54,
	:TSLOT55,
	:TSLOT56,
	:TSLOT57,
	:TSLOT58,
	:TSLOT59,
	:DELA1,
	:DELT1,
	:DELA2,
	:DELT2,
	:DELA3,
	:DELT3,
	:DELA4,
	:DELT4,
	:DELA5,
	:DELT5,
	:SLOT4X,
	:SLOT4R,
	:SLOT4S,
	:SLOT5X,
	:SLOT5R,
	:SLOT5S,
	:FPSSLT2,
	:FPSSLT3,
	:FPSSLT4,
	:FPSSLT5,
	:FPSSLT6,
	:FPSSLT7,
	:FPSSLT8,
	:FPSSLT9,
	:FPSSLT10,
	:FPSSLT11,
	:FPSSLT12,
	:FPSSLT13,
	:FPSSLT14,
	:FPSSLT15,
	:FPSSLT16,
	:FPSSLT17,
	:FPSSLT18,
	:FPSSLT19,
	:FPSSLT20,
	:FPSSLT21,
	:FPSSLT22,
	:FPSSLT23,
	:FPSSLT24,
	:FPSSLT25,
	:FPSPROC,
	:MFILE1,
	:MFILE2,
	:MFILE3,
	:MFILE4,
	:MFILE5,
	:MFILE6,
	:EITOOL1,
	:EITOOL2,
	:EITOOL3,
	:EITOOL4,
	:T_ORIG,
	:TC_ORIG,
	:C_ORIG,
	:BC_ORIG,
	:B_ORIG,
	:HR_ORIG,
	:HOUR,
	:MINUTE,
	:SECOND,
	:MIN_ORIG,
	:SEC_ORIG,
	:FLW_ORIG,
	:WID3NUM,
	:WID4NUM,
	:WID5NUM,
	:ADDNOTE,
	:PART,
	:DELTA,
	:EILOT7,
	:EILOT8,
	:EILOT9,
	:EILOT10,
	:EILOT11,
	:EILOT12,
	:EILOT13,
	:EILOT14,
	:EILOT15,
	:EILOT16,
	:EILOT17,
	:EILOT18,
	:EILOT19,
	:EILOT20,
	:EILOT21,
	:EILOT22,
	:EILOT23,
	:EILOT24,
	:EILOT25,
	:BLABEL11,
	:BLABEL12,
	:BLABEL13,
	:BLABEL14,
	:BLABEL15,
	:BLABEL16,
	:TOOLOUT1,
	:TOOLOUT2,
	:TOOLOUT3,
	:TOOLOUT4,
	:TOOLOUT5,
	:W1ADDER P7UNIT1,
	:W2ADDER P8UNIT1,
	:W1AREA P9UNIT1,
	:W2AREA P10UNIT1,
	:STAGE,
	:STAGE2,
	:STAGE3,
	:STAGE4,
	:STAGE5,
	:STAGE6,
	:STAGE7,
	:LBKOWNER,
	:T_OLD,
	:TC_OLD,
	:C_OLD,
	:BC_OLD,
	:B_OLD,
	:FURNACE,
	:SEND2APC,
	:FTOOL,
	:EITYPE,
	:EI_EQPID,
	:EI_EQPTP,
	:BTCHTM,
	:BTCHTYPE,
	:PPID,
	:EILOT1,
	:EILOT2,
	:EILOT3,
	:EILOT4,
	:EILOT5,
	:EILOT6,
	:FURNACE,
	:SEND2APC,
	:FTOOL,
	:MTHICK1,
	:EITYPE,
	:EI_EQPID,
	:EI_EQPTP,
	:BTCHTM,
	:BTCHTYPE,
	:PPID,
	:EILOT1,
	:EILOT2,
	:EILOT3,
	:EILOT4,
	:EILOT5,
	:EILOT6,
	:EITSTWFR,
	:TWREQ,
	:OPROCESS,
	:OBATCH,
	:POOLED,
	:PLBATCH,
	:EDTUSR,
	:PARTHIDE,
	:EQUIP,
	:NIDC,
	:BLABEL1,
	:BLABEL2,
	:BLABEL3,
	:BLABEL4,
	:BLABEL5,
	:BLABEL6,
	:BLABEL7,
	:BLABEL8,
	:BLABEL9,
	:BLABEL10,
	:DSA_MODE,
	:PR_STPID,
	:PS_STPID,
	:DSAOLTOL,
	:KLSCRIPT,
	:PREDATE,
	:PRETIME,
	:POSTDATE,
	:POSTTIME,
	:KLLOTD1,
	:KLLOTD2,
	:KLLOTD3,
	:KLLOTD4,
	:KLLOTD5,
	:KLLOTD6,
	:KLLOTD7,
	:KLLOTD8,
	:KLLOTD9,
	:KLW1D1,
	:KLW1D2,
	:KLW1D3,
	:KLW1D4,
	:KLW1D5,
	:KLW2D1,
	:KLW2D2,
	:KLW2D3,
	:KLW2D4,
	:KLW2D5,
	:KLSND1,
	:KLSND2,
	:KLSND3,
	:KLSND4,
	:KLSND5,
	:KLSND6,
	:KLBNW1,
	:KLBNW2,
	:FPSSLT1,
	:GOF_AS P11UNIT1,
	:GOF_AS P11UNIT2,
	:GOF_AS P11UNIT3,
	:GOF_AS P11UNIT4,
	:GOF_AS P11UNIT5,
	:ASOFFSET,
	:ASRTYPE,
	:EIRTYPE,
	:RSLOT11,
	:RSLOT12,
	:RSLOT13,
	:RSLOT14,
	:RSLOT15,
	:RSLOT16,
	:RSLOT17,
	:RSLOT18,
	:RSLOT19,
	:RSLOT21,
	:RSLOT22,
	:RSLOT23,
	:RSLOT24,
	:RSLOT25,
	:RSLOT26,
	:RSLOT27,
	:RSLOT28,
	:RSLOT29,
	:RSLOT31,
	:RSLOT32,
	:RSLOT33,
	:RSLOT34,
	:RSLOT35,
	:RSLOT36,
	:RSLOT37,
	:RSLOT38,
	:RSLOT39,
	:RSLOT41,
	:RSLOT42,
	:RSLOT43,
	:RSLOT44,
	:RSLOT45,
	:RSLOT46,
	:RSLOT47,
	:RSLOT48,
	:RSLOT49,
	:RSLOT51,
	:RSLOT52,
	:RSLOT53,
	:RSLOT54,
	:RSLOT55,
	:RSLOT56,
	:RSLOT57,
	:RSLOT58,
	:RSLOT59,
	:TWCHECK,
	:FCETWFRS,
	:EIPGM1,
	:EIPGM2,
	:EIPGM3,
	:EIPGM4,
	:EIPGM5,
	:EIPGM6,
	:EIPGM7,
	:EIPGM8,
	:EIPGM9,
	:EIPGM10,
	:EIPGM11,
	:EIPGM12,
	:EIPGM13,
	:EIPGM14,
	:EIPGM15,
	:EIPGM16,
	:EIPGM17,
	:EIPGM18,
	:EIPGM19,
	:EIPGM20,
	:EIPGM21,
	:EIPGM22,
	:EIPGM23,
	:EIPGM24,
	:EIPGM25,
	:TSLOT11,
	:TSLOT12,
	:TSLOT13,
	:TSLOT14,
	:TSLOT15,
	:TSLOT16,
	:TSLOT17,
	:TSLOT18,
	:TSLOT19,
	:TSLOT21,
	:TSLOT22,
	:TSLOT23,
	:TSLOT24,
	:TSLOT25,
	:TSLOT26,
	:TSLOT27,
	:TSLOT28,
	:TSLOT29,
	:TSLOT31,
	:TSLOT32,
	:TSLOT33,
	:TSLOT34,
	:TSLOT35,
	:TSLOT36,
	:TSLOT37,
	:TSLOT38,
	:TSLOT39




);

//Change load size data type
dt:outnote << data type(character);

:THICK P1U1L1 << Set Name("Z1_s1");
:THICK P1U1L2 << Set Name("Z1_s2");
:THICK P1U1L3 << Set Name("Z1_s3");
:THICK P1U1L4 << Set Name("Z1_s4");
:THICK P1U1L5 << Set Name("Z1_s5");
:THICK P1U1L6 << Set Name("Z1_s6");
:THICK P1U1L7 << Set Name("Z1_s7");
:THICK P1U1L8 << Set Name("Z1_s8");
:THICK P1U1L9 << Set Name("Z1_s9");

:THICK P1U2L1 << Set Name("Z2_s1");
:THICK P1U2L2 << Set Name("Z2_s2");
:THICK P1U2L3 << Set Name("Z2_s3");
:THICK P1U2L4 << Set Name("Z2_s4");
:THICK P1U2L5 << Set Name("Z2_s5");
:THICK P1U2L6 << Set Name("Z2_s6");
:THICK P1U2L7 << Set Name("Z2_s7");
:THICK P1U2L8 << Set Name("Z2_s8");
:THICK P1U2L9 << Set Name("Z2_s9");

:THICK P1U3L1 << Set Name("Z3_s1");
:THICK P1U3L2 << Set Name("Z3_s2");
:THICK P1U3L3 << Set Name("Z3_s3");
:THICK P1U3L4 << Set Name("Z3_s4");
:THICK P1U3L5 << Set Name("Z3_s5");
:THICK P1U3L6 << Set Name("Z3_s6");
:THICK P1U3L7 << Set Name("Z3_s7");
:THICK P1U3L8 << Set Name("Z3_s8");
:THICK P1U3L9 << Set Name("Z3_s9");

//Insert new column for mean
dt << New Column("col1_mean", numeric, continuous, formula(Mean(
	:Z1_s1,
	:Z1_s2,
	:Z1_s3,
	:Z1_s4,
	:Z1_s5,
	:Z1_s6,
	:Z1_s7,
	:Z1_s8,
	:Z1_s9)));
	
dt << New Column("col2_mean", numeric, continuous, formula(Mean(
	:Z2_s1,
	:Z2_s2,
	:Z2_s3,
	:Z2_s4,
	:Z2_s5,
	:Z2_s6,
	:Z2_s7,
	:Z2_s8,
	:Z2_s9)));
	
dt << New Column("col3_mean", numeric, continuous, formula(Mean(
	:Z3_s1,
	:Z3_s2,
	:Z3_s3,
	:Z3_s4,
	:Z3_s5,
	:Z3_s6,
	:Z3_s7,
	:Z3_s8,
	:Z3_s9)));
	
//Cal std dev for batch
dt << New Column("Batch_std", numeric, continuous, formula(StdDev(
	:Z1_s1,
	:Z1_s2,
	:Z1_s3,
	:Z1_s4,
	:Z1_s5,
	:Z1_s6,
	:Z1_s7,
	:Z1_s8,
	:Z1_s9,
	:Z2_s1,
	:Z2_s2,
	:Z2_s3,
	:Z2_s4,
	:Z2_s5,
	:Z2_s6,
	:Z2_s7,
	:Z2_s8,
	:Z2_s9,
	:Z3_s1,
	:Z3_s2,
	:Z3_s3,
	:Z3_s4,
	:Z3_s5,
	:Z3_s6,
	:Z3_s7,
	:Z3_s8,
	:Z3_s9
	)));

	
dt << New Column("TW_count", numeric, nominal, formula(If( Is Missing( :col3_mean ),
	2,
	3
)));

dt << New Column("Batch_Mean", numeric, continuous, formula(:THICK P1RSLTX));

dt << New Column("top_mean", numeric, continuous, formula(:col1_mean));

dt << New Column("center_mean", numeric, continuous, formula(If( Is Missing( :col3_mean ),
	,
	:col2_mean)));

dt << New Column("bottom_mean", numeric, continuous, formula(If( Is Missing( :col3_mean ),
	:col2_mean,
	:col3_mean
)));

//Calc range
//Zone 1
dt << New Column("zone1_max", numeric, continuous, formula(Max(
	:Z1_s1,
	:Z1_s2,
	:Z1_s3,
	:Z1_s4,
	:Z1_s5,
	:Z1_s6,
	:Z1_s7,
	:Z1_s8,
	:Z1_s9)));
	
dt << New Column("zone1_min", numeric, continuous, formula(Min(
	:Z1_s1,
	:Z1_s2,
	:Z1_s3,
	:Z1_s4,
	:Z1_s5,
	:Z1_s6,
	:Z1_s7,
	:Z1_s8,
	:Z1_s9)));
	
dt << New Column("zone1_range", numeric, continuous, formula(:zone1_max - :zone1_min));

//Zone 2
dt << New Column("zone2_max", numeric, continuous, formula(Max(
	:Z2_s1,
	:Z2_s2,
	:Z2_s3,
	:Z2_s4,
	:Z2_s5,
	:Z2_s6,
	:Z2_s7,
	:Z2_s8,
	:Z2_s9)));
	
dt << New Column("zone2_min", numeric, continuous, formula(Min(
	:Z2_s1,
	:Z2_s2,
	:Z2_s3,
	:Z2_s4,
	:Z2_s5,
	:Z2_s6,
	:Z2_s7,
	:Z2_s8,
	:Z2_s9)));
	
dt << New Column("zone2_range", numeric, continuous, formula(:zone2_max - :zone2_min));

//Zone 3
dt << New Column("zone3_max", numeric, continuous, formula(Max(
	:Z3_s1,
	:Z3_s2,
	:Z3_s3,
	:Z3_s4,
	:Z3_s5,
	:Z3_s6,
	:Z3_s7,
	:Z3_s8,
	:Z3_s9)));
	
dt << New Column("zone3_min", numeric, continuous, formula(Min(
	:Z3_s1,
	:Z3_s2,
	:Z3_s3,
	:Z3_s4,
	:Z3_s5,
	:Z3_s6,
	:Z3_s7,
	:Z3_s8,
	:Z3_s9)));
	
dt << New Column("zone3_range", numeric, continuous, formula(:zone3_max - :zone3_min));
	
//Move range columns
dt << Move Selected Columns({"zone1_range"}, To Last);
dt << Move Selected Columns({"zone2_range"}, To Last);
dt << Move Selected Columns({"zone3_range"}, To Last);



dt << New Column("Top_R", numeric, continuous, formula(:zone1_range));

dt << New Column("Center_R", numeric, continuous, formula(If( Is Missing( :zone3_range ),
	,
	:zone2_range)));

dt << New Column("Bottom_R", numeric, continuous, formula(If( Is Missing( :zone3_range ),
	:zone2_range,
	:zone3_range
)));

//simple If statement
dt << new column("Run_Type", character, formula(
	If( :OUTNOTE == "0",
	"TR",
	"PRD"
)));

//Capitalize MTHICK column
For(k = 1, k <= N Rows (dt), k++,
	Column( dt, "MTHICK" )[k] = UPPERCASE( Column( dt, "MTHICK")[k] ));
	
//metro tool	
dt << New Column("MTHICK_2", character, nominal, formula(Match(:MTHICK, 
	"DA01FE", "DA01FEIV",
	"DA01", "DA01FEIV",
	"DB03AS", "DB03ASET",
	"DB03", "DB03ASET",
	"UDFM", "UDFM03",
	"DC01FE", "DC01FEIV",
	"DC01", "DC01FEIV",
	"DA01FEIV", "DA01FEIV",	
	"DB03ASET", "DB03ASET",
	"UDFM03", "UDFM03",
	"DC01FEIV", "DC01FEIV",
)));

//move new metro tool column
dt << Move Selected Columns( {:MTHICK_2}, after(:MTHICK));

//label alternate recipes
dt << New Column("Alt1", character, nominal, formula(
		If(contains(:MFILE9, "QTXVPD"),
			"_QTXVPD",
			If(contains(:MFILE9, "VPD"),
				"_VPD",
				If(contains(:MFILE9, "5TW"),
					"_5TW",
					If(contains(:MFILE9, "3TW"),
						"_3TW",
						If(contains(:MFILE9, "QTX"),
							"_QTX",
							"")))))));
dt << New Column("Alt_Recipe", character, nominal, formula( :Process || :Alt1));


//Graph for batch data
Graph Builder(
	Variables(
		X( :STOP ),
		Y( :Batch_Mean ),
		Y( :Batch_std ),
		Group X( :PROCESS ),
		Overlay( :LOGBOOK )
	),
	Elements( Position( 1, 1 ), Points( X, Y, Legend( 13 ) ) ),
	Elements( Position( 1, 2 ), Points( X, Y, Legend( 15 ) ) ),
	SendToReport(
		Dispatch(
			{},
			"STOP",
			ScaleBox,
			{Label Row( Label Orientation( "Angled" ) )}
		),
		Dispatch(
			{},
			"Batch_Mean",
			ScaleBox,
			{Min( mn ), Max( mx ), Inc( inc ),
			Add Ref Line( ucl, "Solid", "Black", "UCL", 1 ),
			Add Ref Line( ct, "Solid", "Black", "CT", 1 ),
			Add Ref Line( lcl, "Solid", "Black", "LCL", 1 )}
		),
		Dispatch(
			{},
			"Batch_std",
			ScaleBox,
			{Add Ref Line( std, "Solid", "Black", "SL", 1 )}
		),
		Dispatch( {}, "graph title", TextEditBox, {Set Text( "Batch Thk" )} )
	)
);


Graph Builder(
	Size( 570, 718 ),
	Variables(
		X( :STOP ),
		Y( :top_mean ),
		Y( :center_mean ),
		Y( :bottom_mean ),
		Group X( :PROCESS ),
		Overlay( :LOGBOOK )
	),
	Elements( Position( 1, 1 ), Points( X, Y, Legend( 7 ) ) ),
	Elements( Position( 1, 2 ), Points( X, Y, Legend( 8 ) ) ),
	Elements( Position( 1, 3 ), Points( X, Y, Legend( 10 ) ) ),
	SendToReport(
		Dispatch(
			{},
			"STOP",
			ScaleBox,
			{Label Row( Label Orientation( "Angled" ) )}
			),
		Dispatch(
			{},
			"top_mean",
			ScaleBox,
			{Min( mn ), Max( mx ), Inc( inc ), Minor Ticks( 0 ),
			Add Ref Line( ucl, "Solid", "Medium Dark Red", "UCL", 2 ),
			Add Ref Line( ct, "Solid", "Black", "CT", 2 ),
			Add Ref Line( lcl, "Solid", "Medium Dark Red", "LCL", 2 )}
		),
		Dispatch(
			{},
			"center_mean",
			ScaleBox,
			{Min( mn ), Max( mx ), Inc( inc ), Minor Ticks( 0 ),
			Add Ref Line( ucl, "Solid", "Medium Dark Red", "UCL", 2 ),
			Add Ref Line( ct, "Solid", "Black", "CT", 2 ),
			Add Ref Line( lcl, "Solid", "Medium Dark Red", "LCL", 2 )}
		),
		Dispatch(
			{},
			"bottom_mean",
			ScaleBox,
			{Min( mn ), Max( mx ), Inc( inc ), Minor Ticks( 0 ),
			Add Ref Line( ucl, "Solid", "Medium Dark Red", "UCL", 2 ),
			Add Ref Line( ct, "Solid", "Black", "CT", 2 ),
			Add Ref Line( lcl, "Solid", "Medium Dark Red", "LCL", 2 )}
		),
		Dispatch( {}, "graph title", TextEditBox, {Set Text("THK, A")});
	)
);


close(dt2);
close(dtSubset);
