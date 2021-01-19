# OpenGL

#include <stdlib.h>
#include "glut.h"
#include "gl.h"
#include "glu.h"
#include <math.h>


double me_x = 0, me_y = 0, me_z = 0.5; //目の座標
double delta = 0.00; //移動量
int flag1[200] = { 0 }, flag2[200] = { 0 }, flag3[200] = { 0 }, flag4[200] = { 0 }, flaga, flagb, flagc, flagd;
int flagspace = 1;
double i = 0.0;
double a = 0.0;
//環境光の設定
void SetAmbient(float a, float b, float c)
{
	float ambient[] = { a,b,c,1.0 };
	glMaterialfv(GL_FRONT, GL_AMBIENT, ambient);
}

//拡散反射光の設定
void SetDiffuse(float a, float b, float c)
{
	float diffuse[] = { a, b, c, 1.0 };
	glMaterialfv(GL_FRONT, GL_DIFFUSE, diffuse);
}

//鏡面反射光の設定
void SetSpecular(float a, float b, float c)
{
	float specular[] = { a,b,c,1.0 };
	glMaterialfv(GL_FRONT, GL_SPECULAR, specular);
}

//鏡面反射光の鋭さの設定
void SetShineness(float a)
{
	glMaterialf(GL_FRONT, GL_SHININESS, a);
}

void bullion(double a, double b)
{
	int i;
	SetDiffuse(4.05 / 10, 2.95 / 10, 2.0 / 10);//拡散反射光の設定
	glBegin(GL_POLYGON);
	glColor3f(1.0, 1.0, 0.0);
	glVertex3f(a - 0.1, b + 0.3, -2.99);
	glVertex3f(a + 0.1, b + 0.3, -2.99);
	glVertex3f(a, b, -2.99);
	glEnd();

	SetDiffuse(0.2, 1.0, 0.2);//拡散反射光の設定
	glBegin(GL_POLYGON);
	glColor3f(1.0, 1.0, 0.0);
	for (i = 0; i < 700; i++) {
		glVertex3f(a + 0.1 * sin(i * 0.01), b + 0.4 + 0.1 * cos(i * 0.01), -2.99);
	}
	glEnd();
}

void square(double a, double b, double c, double d, int e)
{
	glBegin(GL_POLYGON);
	glColor3f(1.0, 1.0, 0.0);
	glVertex3f(a, b, -2.99);
	glVertex3f(a, b + 0.2, -2.99);
	glVertex3f(a + 0.2, b + 0.2, -2.99);
	glVertex3f(a + 0.2, b, -2.99);
	glEnd();
	//あたり判定　ここから
	if ((((c - 0.06 >= a) && (c - 0.06 <= a + 0.2)) || ((c + 0.06 >= a) && (c + 0.06 <= a + 0.2))) && ((d <= b + 0.2) && (d >= b))) flag1[e] = 1;
	else flag1[e] = 0;
	if ((((c - 0.06 >= a) && (c - 0.06 <= a + 0.2)) || ((c + 0.06 >= a) && (c + 0.06 <= a + 0.2))) && ((d + 0.5 <= b + 0.2) && (d + 0.5 >= b))) flag2[e] = 1;
	else flag2[e] = 0;
	if ((((d + 0.46 >= b) && (d + 0.46 <= b + 0.2)) || ((d + 0.17 >= b) && (d + 0.17 <= b + 0.2)) || ((d >= b + 0.04) && (d <= b + 0.17)) || ((d + 0.34 >= b) && (d + 0.34 <= b + 0.2))) && ((c - 0.1 <= a + 0.2) && (c - 0.1 >= a))) flag3[e] = 1;
	else flag3[e] = 0;
	if ((((d + 0.46 >= b) && (d + 0.46 <= b + 0.2)) || ((d >= b + 0.04) && (d <= b + 0.17)) || ((d + 0.17 >= b) && (d + 0.17 <= b + 0.2)) || ((d + 0.34 >= b) && (d + 0.34 <= b + 0.2))) && ((c + 0.1 <= a + 0.2) && (c + 0.1 >= a))) flag4[e] = 1;
	else flag4[e] = 0;
	//あたり判定　ここまで

}

void dokan(double a, double b, double c, double d, int e)
{


	glBegin(GL_POLYGON);
	glColor3f(0.08, 0.9, 0.2);
	glVertex3f(+a, +b, -2.99);
	glVertex3f(+a, 1.0 + b, -2.98);
	glVertex3f(0.5 + a, 1.0 + b, -2.98);
	glVertex3f(0.5 + a, +b, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.01, 1.0, 0.2);
	glVertex3f(-0.2 + a, 1.0 + b, -2.99);
	glVertex3f(-0.2 + a, 1.1 + b, -2.98);
	glVertex3f(0.7 + a, 1.1 + b, -2.98);
	glVertex3f(0.7 + a, 1.0 + b, -2.99);
	glEnd();
	//あたり判定　ここから
	if ((((c - 0.06 >= a) && (c - 0.06 <= a + 0.2)) || ((c + 0.06 >= a) && (c + 0.06 <= a + 0.2))) && ((d <= b + 0.2) && (d >= b))) flag1[e] = 1;
	else flag1[e] = 0;
	if ((((c - 0.06 >= a) && (c - 0.06 <= a + 0.2)) || ((c + 0.06 >= a) && (c + 0.06 <= a + 0.2))) && ((d + 0.5 <= b + 0.2) && (d + 0.5 >= b))) flag2[e] = 1;
	else flag2[e] = 0;
	if ((((d + 0.46 >= b) && (d + 0.46 <= b + 0.2)) || ((d + 0.17 >= b) && (d + 0.17 <= b + 0.2)) || ((d >= b + 0.04) && (d <= b + 0.17)) || ((d + 0.34 >= b) && (d + 0.34 <= b + 0.2))) && ((c - 0.1 <= a + 0.2) && (c - 0.1 >= a))) flag3[e] = 1;
	else flag3[e] = 0;
	if ((((d + 0.46 >= b) && (d + 0.46 <= b + 0.2)) || ((d >= b + 0.04) && (d <= b + 0.17)) || ((d + 0.17 >= b) && (d + 0.17 <= b + 0.2)) || ((d + 0.34 >= b) && (d + 0.34 <= b + 0.2))) && ((c + 0.1 <= a + 0.2) && (c + 0.1 >= a))) flag4[e] = 1;
	else flag4[e] = 0;
	//あたり判定　ここまで
};

void killer1(double a, double b, double c, double d, int e)
{
	glBegin(GL_POLYGON);
	glColor3f(0.3, 0.3, 0.3);
	for (i = 0; i <= 700; i++)
	{
		glVertex3f(0.16 * cos(0.01 * i) - a + 20.05, 0.16 * sin(0.01 * i) + b + 0.05 - 2, -2.99);

	}
	glEnd();

	//あたり判定　ここから
	if ((((c - 0.06 >= a) && (c - 0.06 <= a + 0.2)) || ((c + 0.06 >= a) && (c + 0.06 <= a + 0.2))) && ((d <= b + 0.2) && (d >= b))) flag1[e] = 1;
	else flag1[e] = 0;
	if ((((c - 0.06 >= a) && (c - 0.06 <= a + 0.2)) || ((c + 0.06 >= a) && (c + 0.06 <= a + 0.2))) && ((d + 0.5 <= b + 0.2) && (d + 0.5 >= b))) flag2[e] = 1;
	else flag2[e] = 0;
	if ((((d + 0.46 >= b) && (d + 0.46 <= b + 0.2)) || ((d + 0.17 >= b) && (d + 0.17 <= b + 0.2)) || ((d >= b + 0.04) && (d <= b + 0.17)) || ((d + 0.34 >= b) && (d + 0.34 <= b + 0.2))) && ((c - 0.1 <= a + 0.2) && (c - 0.1 >= a))) flag3[e] = 1;
	else flag3[e] = 0;
	if ((((d + 0.46 >= b) && (d + 0.46 <= b + 0.2)) || ((d >= b + 0.04) && (d <= b + 0.17)) || ((d + 0.17 >= b) && (d + 0.17 <= b + 0.2)) || ((d + 0.34 >= b) && (d + 0.34 <= b + 0.2))) && ((c + 0.1 <= a + 0.2) && (c + 0.1 >= a))) flag4[e] = 1;
	else flag4[e] = 0;
	//あたり判定　ここまで

}
void killer2(double a, double b, double c, double d, int e)
{
	glBegin(GL_POLYGON);
	glColor3f(0.3, 0.3, 0.3);

	glVertex3f(20.5 - a, 0.3 + b - 2, -2.98);
	glVertex3f(20.5 - a, +b - 2, -2.99);
	glVertex3f(20 - a, +b - 2, -2.99);
	glVertex3f(20 - a, 0.3 + b - 2, -2.98);
	glEnd();

	//あたり判定　ここから
	if ((((c - 0.06 >= a) && (c - 0.06 <= a + 0.2)) || ((c + 0.06 >= a) && (c + 0.06 <= a + 0.2))) && ((d <= b + 0.2) && (d >= b))) flag1[e] = 1;
	else flag1[e] = 0;
	if ((((c - 0.06 >= a) && (c - 0.06 <= a + 0.2)) || ((c + 0.06 >= a) && (c + 0.06 <= a + 0.2))) && ((d + 0.5 <= b + 0.2) && (d + 0.5 >= b))) flag2[e] = 1;
	else flag2[e] = 0;
	if ((((d + 0.46 >= b) && (d + 0.46 <= b + 0.2)) || ((d + 0.17 >= b) && (d + 0.17 <= b + 0.2)) || ((d >= b + 0.04) && (d <= b + 0.17)) || ((d + 0.34 >= b) && (d + 0.34 <= b + 0.2))) && ((c - 0.1 <= a + 0.2) && (c - 0.1 >= a))) flag3[e] = 1;
	else flag3[e] = 0;
	if ((((d + 0.46 >= b) && (d + 0.46 <= b + 0.2)) || ((d >= b + 0.04) && (d <= b + 0.17)) || ((d + 0.17 >= b) && (d + 0.17 <= b + 0.2)) || ((d + 0.34 >= b) && (d + 0.34 <= b + 0.2))) && ((c + 0.1 <= a + 0.2) && (c + 0.1 >= a))) flag4[e] = 1;
	else flag4[e] = 0;
	//あたり判定　ここまで

}

void clear()
{
	double a = 30;
	glBegin(GL_POLYGON);
	glColor3f(1.0, 1.0, 1.0);  //C

	glVertex3f(a, 1.5, -2.99);
	glVertex3f(a, -0.5, -2.99);
	glVertex3f(a + 1.5, -0.5, -2.99);
	glVertex3f(a + 1.5, 1.5, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0, 0.0, 0.0);
	glVertex3f(a + 0.5, 1.0, -2.98);
	glVertex3f(a + 0.5, 0.0, -2.98);
	glVertex3f(a + 1.5, 0.0, -2.98);
	glVertex3f(a + 1.5, 1.0, -2.98);
	glEnd();
	glBegin(GL_POLYGON);  //L
	glColor3f(1.0, 1.0, 1.0);
	glVertex3f(a + 2, 1.5, -2.99);
	glVertex3f(a + 2, -0.5, -2.99);
	glVertex3f(a + 2.5, -0.5, -2.99);
	glVertex3f(a + 2.5, 1.5, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	glVertex3f(a + 2.5, -0.5, -2.99);
	glVertex3f(a + 2.5, 0, -2.99);
	glVertex3f(a + 3.5, 0, -2.99);
	glVertex3f(a + 3.5, -0.5, -2.99);
	glEnd();

	glBegin(GL_POLYGON);//E
	glVertex3f(a + 4, 1.5, -2.99);
	glVertex3f(a + 4, -0.5, -2.99);
	glVertex3f(a + 4.5, -0.5, -2.99);
	glVertex3f(a + 4.5, 1.5, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	glVertex3f(a + 4.5, 1.5, -2.99);
	glVertex3f(a + 4.5, 1.0, -2.99);
	glVertex3f(a + 5.5, 1.0, -2.99);
	glVertex3f(a + 5.5, 1.5, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	glVertex3f(a + 4.5, 0.75, -2.99);
	glVertex3f(a + 4.5, 0.25, -2.99);
	glVertex3f(a + 5.5, 0.25, -2.99);
	glVertex3f(a + 5.5, 0.75, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	glVertex3f(a + 4.5, 0.0, -2.99);
	glVertex3f(a + 4.5, -0.5, -2.99);
	glVertex3f(a + 5.5, -0.5, -2.99);
	glVertex3f(a + 5.5, 0.0, -2.99);
	glEnd();
	glBegin(GL_POLYGON); //A
	glVertex3f(a + 7, 1.5, -2.99);
	glVertex3f(a + 7.5, 1.5, -2.99);
	glVertex3f(a + 6.5, -0.5, -2.99);
	glVertex3f(a + 6, -0.5, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	glVertex3f(a + 7, 1.5, -2.99);
	glVertex3f(a + 7.5, 1.5, -2.99);
	glVertex3f(a + 8.5, -0.5, -2.99);
	glVertex3f(a + 8.0, -0.5, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	glVertex3f(a + 6.7, 0.7, -2.99);
	glVertex3f(a + 6.7, 0.3, -2.99);
	glVertex3f(a + 7.7, 0.3, -2.99);
	glVertex3f(a + 7.7, 0.7, -2.99);
	glEnd();//R
	glBegin(GL_POLYGON);
	glVertex3f(a + 9, 1.5, -2.99);
	glVertex3f(a + 9, -0.5, -2.99);
	glVertex3f(a + 9.5, -0.5, -2.99);
	glVertex3f(a + 9.5, 1.5, -2.99);
	glEnd();
	glBegin(GL_POLYGON);
	for (i = 0; i < 700; i++) {
		glVertex3f(a + 9.7 + 0.7 * sin(i * 0.01), 0.82 + 0.7 * cos(i * 0.01), -2.98);
	}
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(0.0, 0.0, 0.0);
	for (i = 0; i < 700; i++) {
		glVertex3f(a + 9.75 + 0.2 * sin(i * 0.01), 0.82 + 0.2 * cos(i * 0.01), -2.97);
	}
	glEnd();
	glBegin(GL_POLYGON);
	glColor3f(1.0, 1.0, 1.0);
	glVertex3f(a + 9.5, 0.5, -2.99);
	glVertex3f(a + 10, 0.5, -2.99);
	glVertex3f(a + 11, -0.5, -2.99);
	glVertex3f(a + 10.5, -0.5, -2.99);
	glEnd();
}

void display(void)
{
	//double temp_x,temp_y,temp_z,temp_dis;
	//double ue_x, ue_y, ue_z;
	GLdouble housen[] = { 0,0,1 };
	int i;

	flaga = 0;
	flagb = 0;
	flagc = 0;
	flagd = 0;


	glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
	glPushMatrix();
	gluLookAt(me_x, 0, 3, me_x, 0, -3, 0, 1, 0); //ここを編集して良い

		//ここに描きたい物を書く．
	glEnable(GL_DEPTH_TEST);
	//下限　ここから
	glBegin(GL_POLYGON);
	glColor3f(1.0, 1.0, 0.0);
	glVertex3f(-3.0, -2.0, -2.99);
	glVertex3f(-3.0, -1.8, -2.99);
	glVertex3f(150.0, -1.8, -2.99);
	glVertex3f(150.0, -2.0, -2.99);
	glEnd();

	if (me_y <= -1.8) flag1[0] = 1;
	else flag1[0] = 0;
	//下限　ここまで

	//上限　ここから
	glBegin(GL_POLYGON);
	glColor3f(1.0, 1.0, 0.0);
	glVertex3f(-3.0, 2.0, -2.99);
	glVertex3f(-3.0, 1.8, -2.99);
	glVertex3f(150.0, 1.8, -2.99);
	glVertex3f(150.0, 2.0, -2.99);
	glEnd();

	if (me_y + 0.5 >= 1.8) flag2[0] = 1;
	else flag2[0] = 0;
	//上限　ここまで

	if (me_x - 0.1 <= -2.98) flag3[0] = 1;
	else flag3[0] = 0;


	//背面　ここから
	SetDiffuse(0.0, 0.0, 0.0);//拡散反射光の設定
	glBegin(GL_POLYGON);
	glColor3f(0.0, 0.0, 0.0);
	glVertex3f(-3.0, -2.0, -3.0);
	glVertex3f(-3.0, 2.0, -3.0);
	glVertex3f(150.0, 2.0, -3.0);
	glVertex3f(150.0, -2.0, -3.0);
	glEnd();
	//背面　ここまで



	square(0.5, 0, me_x, me_y, 50);
	square(0.7, 0.2, me_x, me_y, 51);
	bullion(me_x, me_y);
	dokan(4.0, -2.0, me_x, me_y, 52);

	killer1(a, 0.6, me_x, me_y, 53);
	killer2(a, 0.5, me_x, me_y, 54);
	clear();

	for (i = 0; i < 200; i++)
	{
		flaga = flaga + flag1[i];
		flagb = flagb + flag2[i];
		flagc = flagc + flag3[i];
		flagd = flagd + flag4[i];
	}

	glEnable(GL_LIGHTING);
	//ここに描く

	glPopMatrix();
	glDisable(GL_LIGHTING);
	glDisable(GL_DEPTH_TEST);
	//glFlush();
	glutSwapBuffers();
}



//------------------------------------
//特殊キーに対するコールバック関数
//------------------------------------

void TouchKey_S(int key, int x, int y)
{
	switch (key) {
	case GLUT_KEY_LEFT:
		if (flagc == 0) me_x = me_x - 0.04;
		break;
	case GLUT_KEY_RIGHT:
		if (flagd == 0)	me_x = me_x + 0.04;
		break;
	case GLUT_KEY_DOWN:

		break;
	case GLUT_KEY_UP:

		break;
	case GLUT_KEY_F1:
		//me_x=0.0;
		//me_y=0.0;
		//me_z=0.5;
		//flag = 1;
		break;
	}
	//if ((me_x < -1.5) || (1.5 < me_x)) flag=0; //ゲームオーバー
	glutPostRedisplay();
}

//------------------------------------
//通常のキーに対するコールバック関数
//------------------------------------

void TouchKey_N(unsigned char key, int x, int y)
{
	switch (key) {
	case 'z':

		break;
	case 'x':
		delta = 0.05;
		break;
	}
	glutPostRedisplay();
}

void myInit(char* progname)
{
	int width = 700, height = 700;
	float aspect = (float)width / (float)height;

	glutInitWindowPosition(0, 0);
	glutInitWindowSize(width, height);
	//glutInitDisplayMode( GLUT_RGBA | GLUT_DEPTH);
	glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGBA);

	glutCreateWindow(progname);

	glClearColor(0.0, 0.5, 1.0, 1.0);
	glutSpecialFunc(TouchKey_S);
	glutKeyboardFunc(TouchKey_N);

	glMatrixMode(GL_PROJECTION);
	glLoadIdentity();
	gluPerspective(45.0, aspect, 0.1, 40.0);
	glMatrixMode(GL_MODELVIEW);
	glEnable(GL_LIGHT0);
}

void idle(void)
{
	me_y += delta;
	if (flaga == 0) {
		delta -= 0.0001;
	}
	else delta = 0;
	a += 0.005;
	glutPostRedisplay();
}


int main(int argc, char** argv)
{
	//Data_set();//障害物の座標の決定
	glutInit(&argc, argv);
	myInit(argv[0]);
	glutDisplayFunc(display);
	glutIdleFunc(idle);
	glutMainLoop();
	return(0);
}
//glVertex3f(cos(0.01*i),sin(0.01*i)+0.1*sin(0.01*a),-2.99);//綺麗な円
